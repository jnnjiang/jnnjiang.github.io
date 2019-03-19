---
title: Android-sqlite
permalink: Android-sqlite
toc: false
date: 2019-03-19 13:49:52
tags:
categories:
---
我们创建数据库一般就是集成 SQLiteHelper ，在构造方法把 DB_NAME 
传进入，就会默认在 data/data/<`package_name>/database/ 下创建，

String path = "mtp/aaa.db";
        SQLiteDatabase mDb = SQLiteDatabase.openOrCreateDatabase(path ,null);

在指定路径下创建
SQLiteCantOpenDatabaseException: unknown error (code 14): Could not open database

调用 openOrCreateDatabase 时候，该路径下文件不存在的时候，不会默认帮我们创建，所以打不开数据库，因为没有这个数据库，只要手动创建了文件，然后就没问题了。



        String path = "mtp/AAA";
        File pathFile = new File(path);
        File file = new File(path+"/aa.db");
        try{
            if(!pathFile.exists()){
                pathFile.mkdirs();
            }
            if(!file.exists()){
                file.createNewFile();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        SQLiteDatabase mDb = SQLiteDatabase.openOrCreateDatabase(file,null);