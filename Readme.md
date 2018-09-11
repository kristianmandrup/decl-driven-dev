# Declarative Driven Development

## Select environments to use

- local
- remote

Development Workflow

- dev
- test
- staging
- prod

## Select adapter to use for each environment

At any time you can add or update domain entities

## Define entities and data

Use CLI to create, delete or update entities

- Connect to entity repos (collections of predefined entities)
- Select entity from list (or create custom)
- Select properties to use (customize)

Update will take existing entity and ask you to add, delete or change properties

### CLI examples

```bash
$ entity new user
User entity
select properties:
- name
- firstName [string] (first name)
- lastName [string] (last name)
- middleName [string] (middle name)
- age [integer]
- birthday [date]
- role [string]
- ...
```

Use entity resource retrieved from URL

`$ entity new user -r bit.ly/abc123`

Or use alias to resource (from local mapping to URL)

`$ entity new user -a my-user`

## Properties

Each Entity may always have:

- ID (unique)
- owner (user who created it)
- refs (to other entities in app model)
- timestamps
  - created
  - updated

Each Entity generates:

- `entities/entity/[entity]-def.yml` file
- `entities/entity/data/[entity].json` sample data (using faker)
- `entities/entity/schema/[entity]-schema.json` JSON schema
- `entities/entity/schema/[entity]-schema.test.js` JSON schema test using sample data file
- ...

See more:

- [Entity](./entities/Entity.md)
- [JSON conversions](./entities/JSON.md)

## Generate

- Generate schemas
- Generate tests

## Entity Types

Select the types of Entity available

- Object
- Collection (implies Object as well)

## Entity Actions

For an entity define actions that can be performed

### Object

- Update
- Delete
- Toggle (boolean)
- Increment (number)
- Decrement (number)
- AddChild
- RemoveChild

### Collection

- Add
- Remove (index)

## Entity Views

- View Obj (list of properties from single entity)
- View property (such as count of specific child collection)
- List (filter)

## Application

An application primarily consists of the following:

- [Application](./application/Application.md)
- [Displays](./displays/Displays.md)
- [Routes](./routes/Routes.md)
- [Forms](./forms/Forms.md)
- [Session](./session/Session.md)
- [Stores](./stores/Stores.md)
- [APIs](./apis/APIs.md)
- [Validators](./validators/Validators.md)
- [Components](./components/Components.md)
