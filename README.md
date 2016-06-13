# Best Practices

This guide shows you how to get the most out of Generate! 

- create awesome generators
- naming tasks
- naming generators
- micro-generators

## Naming tasks

**Prerequisites**

- Basic understanding of [tasks]()
- Basic understanding of [generators]()
- Basic understanding of [plugins]()

**Overview**

Using good naming practices ensures that your generator will not only be easier to use from the command line, but it will also be easier for other implementors to use your generator as a [sub-generator][] or [plugin][] in their own generators.

 [task documentation](), 

Aliases are also useful for preventing task-naming conflicts in cases where generators are used as plugins, since it's possible for multiple generators to have the same task names. 

providing an alternative name in cases where a generator might be used as a plugin by another generator, _both generators have a task with the same name_. 


```js
// --- one.js ---
module.exports = function(app) {
  app.task('foo', function() {});
  app.task('bar', function() {});
  app.task('default', ['foo', 'bar']);
};

// --- two.js ---
module.exports = function(app) {
  // use generator `one` as a plugin, which adds tasks from
  // `one` to this generator
  app.use(require('./one'));

  // the following tasks will overwrite the tasks from generator `one`
  app.task('foo', function() {});
  app.task('bar', function() {});
  app.task('default', ['foo', 'bar']);
};
```

