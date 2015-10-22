##Mongo commands
---

List databases: ```show dbs```

List collections: ```show collections```

Select a database: ```use [INSERT DB NAME]```

---

Find all elements: ```db.[COLLECTION].find().pretty()```

Find specific element: ```db.[COLLECTION].find({ key: "value" }).pretty()```

Find regex element: ```db.[COLLECTION].find({ key: /value/ }).pretty()```

---

Remove all elements: ```db.[COLLECTION].remove({})```

Alternative is ```db.[COLLECTION].drop()``` (Removes entire collection)

Remove specific element as with find.

---

Update element: ```db.[COLLECTION].update([FIND], [REPLACEMENT])```