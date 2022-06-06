# sequelize-normalization

Sequelize supports the standard associations: One-To-One, One-To-Many and Many-To-Many.

Sequelize provides four types of associations that should be combined to create them:

1. The HasOne association
2. The BelongsTo association
3. The HasMany association
4. The BelongsToMany association

## Defining the Sequelize associations

```js
const A = sequelize.define('A' /* ... */);
const B = sequelize.define('B' /* ... */);

A.hasOne(B); // A HasOne B
A.belongsTo(B); // A BelongsTo B
A.hasMany(B); // A HasMany B
A.belongsToMany(B, { through: 'C' }); // A BelongsToMany B through the junction table C
```

They all accept an options object as a second parameter (optional for the first three, mandatory for belongsToMany containing at least the through property):

```js
A.hasOne(B, {
  /* options */
});
A.belongsTo(B, {
  /* options */
});
A.hasMany(B, {
  /* options */
});
A.belongsToMany(B, { through: 'C' /* options */ });
```

> The order in which the association is defined is relevant. In other words, the order matters, for the four cases.
> In all examples above, `A` is called the source model and `B` is called the target model. This terminology is important.

The `A.hasOne(B)` association means that a `One-To-One` relationship exists between `A and B`, with the foreign key being defined in the target `model (B)`.

The `A.belongsTo(B)` association means that a `One-To-One` relationship exists between `A and B`, with the foreign key being defined in the source `model (A)`.

The `A.hasMany(B)` association means that a `One-To-Many` relationship exists between `A and B`, with the foreign key being defined in the target `model (B)`.

## Creating the standard relationships

- To create a One-To-One relationship, the hasOne and belongsTo associations are used together;

- To create a One-To-Many relationship, the hasMany and belongsTo associations are used together;

- To create a Many-To-Many relationship, two belongsToMany calls are used together.
  > Note: there is also a Super Many-To-Many relationship, which uses six associations at once.

## One-To-One relationships

let's assume that we have two models, Foo and Bar. We want to setup a One-To-One relationship between them such that Bar gets a fooId column.

```js
Foo.hasOne(Bar);
Bar.belongsTo(Foo);
```

This way, calling Bar.sync() after the above will yield the following SQL (on PostgreSQL, for example):

```js
CREATE TABLE IF NOT EXISTS "foos" (
  /* ... */
);
CREATE TABLE IF NOT EXISTS "bars" (
  /* ... */
  "fooId" INTEGER REFERENCES "foos" ("id") ON DELETE SET NULL ON UPDATE CASCADE
  /* ... */
);
```

### onDelete and onUpdate

```js
Foo.hasOne(Bar, {
  onDelete: 'RESTRICT',
  onUpdate: 'RESTRICT',
});
Bar.belongsTo(Foo);
```

> The possible choices are RESTRICT, CASCADE, NO ACTION, SET DEFAULT and SET NULL.

### Customizing the foreign key

```js
// Option 1
Foo.hasOne(Bar, {
  foreignKey: 'myFooId',
});
Bar.belongsTo(Foo);

// Option 2
Foo.hasOne(Bar, {
  foreignKey: {
    name: 'myFooId',
  },
});
Bar.belongsTo(Foo);

// Option 3
Foo.hasOne(Bar);
Bar.belongsTo(Foo, {
  foreignKey: 'myFooId',
});

// Option 4
Foo.hasOne(Bar);
Bar.belongsTo(Foo, {
  foreignKey: {
    name: 'myFooId',
  },
});
```

To use UUID as the foreign key data type instead of the default (INTEGER).

```js
const { DataTypes } = require('Sequelize');

Foo.hasOne(Bar, {
  foreignKey: {
    // name: 'myFooId'
    type: DataTypes.UUID,
  },
});
Bar.belongsTo(Foo);
```

## One-To-Many relationships

we have the models Team and Player. We want to tell Sequelize that there is a One-To-Many relationship between them, meaning that one Team has many Players, while each Player belongs to a single Team.

```js
Team.hasMany(Player);
Player.belongsTo(Team);
```

In PostgreSQL :

```js
CREATE TABLE IF NOT EXISTS "Teams" (
  /* ... */
);
CREATE TABLE IF NOT EXISTS "Players" (
  /* ... */
  "TeamId" INTEGER REFERENCES "Teams" ("id") ON DELETE SET NULL ON UPDATE CASCADE,
  /* ... */
);
```

To change the name of the foreign key and make sure that the relationship is mandatory.

```js
Team.hasMany(Player, {
  foreignKey: 'clubId',
});
Player.belongsTo(Team);
```

## Many-To-Many relationships

we will consider the models `Movie` and `Actor`. One actor may have participated in many movies, and one movie had many actors involved with its production. The junction table that will keep track of the associations will be called `ActorMovies`, which will contain the foreign keys `movieId` and `actorId`.

```js
const Movie = sequelize.define('Movie', { name: DataTypes.STRING });
const Actor = sequelize.define('Actor', { name: DataTypes.STRING });
Movie.belongsToMany(Actor, { through: 'ActorMovies' });
Actor.belongsToMany(Movie, { through: 'ActorMovies' });
```

In PostgreSQL :

```js
CREATE TABLE IF NOT EXISTS "ActorMovies" (
  "createdAt" TIMESTAMP WITH TIME ZONE NOT NULL,
  "updatedAt" TIMESTAMP WITH TIME ZONE NOT NULL,
  "MovieId" INTEGER REFERENCES "Movies" ("id") ON DELETE CASCADE ON UPDATE CASCADE,
  "ActorId" INTEGER REFERENCES "Actors" ("id") ON DELETE CASCADE ON UPDATE CASCADE,
  PRIMARY KEY ("MovieId","ActorId")
);
```

Instead of a string, passing a model directly is also supported, and in that case the given model will be used as the junction model.

```js
const Movie = sequelize.define('Movie', { name: DataTypes.STRING });
const Actor = sequelize.define('Actor', { name: DataTypes.STRING });
const ActorMovies = sequelize.define('ActorMovies', {
  MovieId: {
    type: DataTypes.INTEGER,
    references: {
      model: Movie, // 'Movies' would also work
      key: 'id',
    },
  },
  ActorId: {
    type: DataTypes.INTEGER,
    references: {
      model: Actor, // 'Actors' would also work
      key: 'id',
    },
  },
});
Movie.belongsToMany(Actor, { through: ActorMovies });
Actor.belongsToMany(Movie, { through: ActorMovies });
```

There are three ways to specify a different name for the foreign key :

- By providing the foreign key name directly
- By defining an Alias
- By doing both things

## Special methods

```js
Foo.hasOne(Bar);

-fooInstance.getBar();
-fooInstance.setBar();
-fooInstance.createBar();
```

```js
Foo.belongsTo(Bar);

-fooInstance.getBar();
-fooInstance.setBar();
-fooInstance.createBar();
```

```js
Foo.hasMany(Bar);

-fooInstance.getBars();
-fooInstance.countBars();
-fooInstance.hasBar();
-fooInstance.hasBars();
-fooInstance.setBars();
-fooInstance.addBar();
-fooInstance.addBars();
-fooInstance.removeBar();
-fooInstance.removeBars();
-fooInstance.createBar();
```

```js
Foo.belongsToMany(Bar, { through: Baz });

-fooInstance.getBars();
-fooInstance.countBars();
-fooInstance.hasBar();
-fooInstance.hasBars();
-fooInstance.setBars();
-fooInstance.addBar();
-fooInstance.addBars();
-fooInstance.removeBar();
-fooInstance.removeBars();
-fooInstance.createBar();
```
