---
title: nodejs express学习笔记
date: 2017-03-02 21:06:52
tags:
---
　　<p>打算用Nodejs和Express做一个简单的项目，从零开始一步一步学习nodejs。</p>
## `nodejs`, `mongodb`分页实现
1. 使用`mongoose` `skip`方法实现:
```
exports.pagingBySkip = function (model, pageIndex, pageSize, callback) {
    var modelSchema = mongoose.model(model);
    var query = modelSchema.find();
    if (Number(pageIndex) >= 1 && Number(pageSize) >= 1) {
        query.skip((pageIndex - 1) * Number(pageSize));
        query.limit(Number(pageSize));
    }
    query.exec(function (err, docs) {
        callback(err, docs);
    });
};
```
2. 根据ObjectId获取最后一个，然后获取这个id的下一页，需要实现两个方法:
<!-- more -->
  1. `getLatestObjectId`获取当页最后一个ObjectId
```
var getLatest = function (model, size, callback) {
    var query = model.find();
    query.limit(Number(size));
    query.exec(function (err, docs) {
        var doc = docs[size - 1];
        callback(err, doc);
    })
};
```
  2. `getNextPageWithLastId`获取下一页
```  
var getNextPageWithLastId = function (model, lastId, size, callback) {
    var query = model.find({'_id': {"$gt": lastId}});
    query.limit(Number(size));
    if (undefined != fields || '' != fields) {
        query.select(fields);
    }
    query.exec(function (err, docs) {
        callback(err, docs);
    })
};
```
  3. `paging`主方法
```  
exports.paging = function (model, pageIndex, pageSize, callback) {
    var modelSchema = mongoose.model(model);
    getLatest(modelSchema, (pageIndex - 1) * pageSize, function (err, doc) {
        getNextPageWithLastId(modelSchema, doc._id, pageSize, function (err, docs) {
            callback(err, docs);
        })
    })
};
```

## `mongoose` `update`
官方文档给多种更新方式
1. 根据`ObjectId`使用`findOne`找出这条需要更新的记录，然后保存`save`，保存时会自动使用新值合并这两条记录。  
```
Model.findById(id, function (err, model) {
  if (err) return handleError(err);
  model.size = 'large';
  model.save(function (err, model) {
    if (err) return handleError(err);
    res.send(model);
  });
});
```
2. 直接使用`update`方法`Model.update({ _id: id }, { $set: { size: 'large' }}, callback);`
3. 如果需要参数返回，使用`findByIdAndUpdate`方法   
```
Model.findByIdAndUpdate(id, { $set: { size: 'large' }}, { new: true }, function (err, model) {
  if (err) return handleError(err);
  res.send(model);
});
```
上面方法2,3都可以使用`Validators`进行更新参数校验
---
title: nodejs express学习笔记
date: 2017-03-02 21:06:52
tags:
---
　　<p>打算用Nodejs和Express做一个简单的项目，从零开始一步一步学习nodejs。</p>
## `nodejs`, `mongodb`分页实现
1. 使用`mongoose` `skip`方法实现:
```
exports.pagingBySkip = function (model, pageIndex, pageSize, callback) {
    var modelSchema = mongoose.model(model);
    var query = modelSchema.find();
    if (Number(pageIndex) >= 1 && Number(pageSize) >= 1) {
        query.skip((pageIndex - 1) * Number(pageSize));
        query.limit(Number(pageSize));
    }
    query.exec(function (err, docs) {
        callback(err, docs);
    });
};
```
2. 根据ObjectId获取最后一个，然后获取这个id的下一页，需要实现两个方法:
<!-- more -->
  1. `getLatestObjectId`获取当页最后一个ObjectId
```
var getLatest = function (model, size, callback) {
    var query = model.find();
    query.limit(Number(size));
    query.exec(function (err, docs) {
        var doc = docs[size - 1];
        callback(err, doc);
    })
};
```
  2. `getNextPageWithLastId`获取下一页
```  
var getNextPageWithLastId = function (model, lastId, size, callback) {
    var query = model.find({'_id': {"$gt": lastId}});
    query.limit(Number(size));
    if (undefined != fields || '' != fields) {
        query.select(fields);
    }
    query.exec(function (err, docs) {
        callback(err, docs);
    })
};
```
  3. `paging`主方法
```  
exports.paging = function (model, pageIndex, pageSize, callback) {
    var modelSchema = mongoose.model(model);
    getLatest(modelSchema, (pageIndex - 1) * pageSize, function (err, doc) {
        getNextPageWithLastId(modelSchema, doc._id, pageSize, function (err, docs) {
            callback(err, docs);
        })
    })
};
```

## `mongoose` `update`
官方文档给多种更新方式
1. 根据`ObjectId`使用`findOne`找出这条需要更新的记录，然后保存`save`，保存时会自动使用新值合并这两条记录。  
```
Model.findById(id, function (err, model) {
  if (err) return handleError(err);
  model.size = 'large';
  model.save(function (err, model) {
    if (err) return handleError(err);
    res.send(model);
  });
});
```
2. 直接使用`update`方法`Model.update({ _id: id }, { $set: { size: 'large' }}, callback);`
3. 如果需要参数返回，使用`findByIdAndUpdate`方法   
```
Model.findByIdAndUpdate(id, { $set: { size: 'large' }}, { new: true }, function (err, model) {
  if (err) return handleError(err);
  res.send(model);
});
```
上面方法2,3都可以使用`Validators`进行更新参数校验
