<h1 align="center">Welcome to @mahdad/soft-delete-plugin-mongoose 👋</h1>
<p>
  <a href="https://www.npmjs.com/package/@mahdad/soft-delete-plugin-mongoose" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/@mahdad/soft-delete-plugin-mongoose.svg">
  </a>
  <a href="https://github.com/MahdadGhasemian/mongoose-soft-delete#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/MahdadGhasemian/mongoose-soft-delete/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/MahdadGhasemian/mongoose-soft-delete/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/github/license/bishkou/password-pwnd" />
  </a>
</p>

> a mongoose plugin that allows you to soft delete documents and restore them in MongoDB (for JS & TS)

- **Soft delete your MongoDB documents and restore them**

- **JS and TS**

### 🏠 [Homepage](https://github.com/MahdadGhasemian/mongoose-soft-delete)

## Install

```sh
npm install @mahdad/soft-delete-plugin-mongoose
```

## How It Works

**Javascript Version**

```js
const mongoose = require("mongoose");
const { softDeletePlugin } = require("@mahdad/soft-delete-plugin-mongoose");
const Schema = mongoose.Schema;

const TestSchema = new Schema({
  name: String,
  lastName: String,
});

TestSchema.plugin(softDeletePlugin);
const TestModel = mongoose.model("Test", TestSchema);

const test = new TestModel({ name: "hello", lastName: "world" });

/*** returns an object containing the number of softDeleted elements ***/
/***
    {deleted: number} 
***/
/***
    the argument options is optional
***/
const options = { validateBeforeSave: false };
const deleted = await TestModel.softDelete(
  { _id: test._id, name: test.name },
  options
);
/** 
 const deleted = await Test.softDelete({ _id: test._id, name: test.name }); is also valid
**/

/*** returns an object containing the number of restored elements ***/
/***
    {restored: number} 
***/
const restored = await TestModel.restore({ _id: test._id, name: test.name });

/*** returns all deleted elements ***/
const deletedElements = await TestModel.findDeleted();

/*** returns all available elements (not deleted) ***/
const availableElements = await TestModel.find();

/*** returns one available element (not deleted) ***/
const availableElements = await TestModel.findOne();

/*** update if is not be deleted (not deleted) ***/
const availableElements = await TestModel.findOneAndUpdate();

/*** counts all available elements (not deleted) ***/
const countAvailable = await TestModel.count();

/*** findById returns the document whether deleted or not  ***/
```

**Typescript Version**

```ts
import * as mongoose from 'mongoose';
import { softDeletePlugin, SoftDeleteModel } from '@mahdad/soft-delete-plugin-mongoose';

interface Test extends mongoose.Document {
    name: string;
    lastName: string;
}

const TestSchema = new mongoose.Schema({
    name: String,
    lastName: String
});
TestSchema.plugin(softDeletePlugin);
// two different ways of implementing model depending on technology used
// 1st way
const testModel = mongoose.model<Test, SoftDeleteModel<Test>>('Test', TestSchema);

//2nd way (nestjs way)
constructor(@InjectModel('Test') private readonly testModel: SoftDeleteModel<Test>) {}

const test = await new this.testModel({name: 'hello', lastName: 'world'});

/*** returns an object containing the number of softDeleted elements ***/
/***
    {deleted: number}
***/
/***
    the argument options is optional
***/
const options = { validateBeforeSave: false };
const deleted = await this.testModel.softDelete({ _id: test._id, name: test.name }, options);
/**
 const deleted = await Test.softDelete({ _id: test._id, name: test.name }); is also valid
**/

/*** returns an object containing the number of restored elements ***/
/***
    {restored: number}
***/
const restored = await this.testModel.restore({ _id: test._id, name: test.name });

/*** returns all deleted elements ***/
const deletedElements = await this.testModel.findDeleted();

/*** returns all available elements (not deleted) ***/
const availableElements = await this.testModel.find();

/*** returns one available element (not deleted) ***/
const availableElements = await this.testModel.findOne();

/*** update if is not be deleted (not deleted) ***/
const availableElements = await this.testModel.findOneAndUpdate();

/*** counts all available elements (not deleted) ***/
const countAvailable = await this.testModel.count();

/*** findById returns the document whether deleted or not  ***/
```

## Author

👤 **Nour Karoui This**

- Repository has been forked from [@nour-karoui](https://github.com/nour-karoui/mongoose-soft-delete)

👤 **MahdadGhasemian**

- Github: [@MahdadGhasemian](https://github.com/MahdadGhasemian)
- LinkedIn: [@mahdad-ghasemian](https://www.linkedin.com/in/mahdad-ghasemian/)

## 🤝 Contributing

Contributions, issues and feature requests are welcome!<br />Feel free to check [issues page](https://github.com/MahdadGhasemian/mongoose-soft-delete/issues). You can also take a look at the [contributing guide](https://github.com/MahdadGhasemian/mongoose-soft-delete/blob/master/CONTRIBUTING.md).

## Show your support

Give a [STAR](https://github.com/MahdadGhasemian/mongoose-soft-delete) if this project helped you!

## 📝 License

- Copyright © 2021 [MahdadGhasemian](https://github.com/MahdadGhasemian).
- This project is [MIT](https://github.com/MahdadGhasemian/mongoose-soft-delete/blob/master/LICENSE) licensed.

---

_This README was generated with by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_
