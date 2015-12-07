# Brown Sugar ORM (Sugar + SQLCipher) [![Build Status](https://travis-ci.org/satyan/sugar.svg?branch=master)](https://travis-ci.org/satyan/sugar) [![Coverage Status](https://coveralls.io/repos/satyan/sugar/badge.svg?branch=master)](https://coveralls.io/r/satyan/sugar?branch=master)

[![Join the chat at https://gitter.im/satyan/sugar](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/satyan/sugar?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Insanely easy way to work with Android SQLCipher databases.

Official documentation can be found [here](http://satyan.github.io/sugar). The example application is provided in the **example** folder in the source.

## Features

Sugar ORM was built in contrast to other ORM's to have:

- A simple, concise, and clean integration process with minimal configuration.
- Automatic table and column naming through reflection.
- Support for migrations between different schema versions.

## Installing

There are four ways to install Sugar:

#### As a Gradle dependency

This is the preferred way. Simply add:

```groovy
compile 'com.github.satyan:sugar:1.4'
```

to your project dependencies and run `gradle build` or `gradle assemble`.

#### As a Maven dependency

Declare the dependency in Maven:

```xml
<dependency>
    <groupId>com.github.satyan</groupId>
    <artifactId>sugar</artifactId>
    <version>1.4</version>
</dependency>
```

#### As a library project

Download the source code and import it as a library project in Eclipse. The project is available in the folder **library**. For more information on how to do this, read [here](http://developer.android.com/tools/projects/index.html#LibraryProjects).

#### As a jar

Visit the [releases](https://github.com/satyan/sugar/releases) page to download jars directly. You can drop them into your `libs` folder and configure the Java build path to include the library. See this [tutorial](http://www.vogella.com/tutorials/AndroidLibraryProjects/article.html) for an excellent guide on how to do this.

===================

After installing, check out how to set up your first database and models [here](http://satyan.github.io/sugar/getting-started.html).

## Examples
### SugarRecord
```
public class Book extends SugarRecord {
  @Unique
  String isbn;
  String title;
  String edition;

  // Default constructor is necessary for SugarRecord
  public Book() {

  }

  public Book(String isbn, String title, String edition) {
    this.isbn = isbn;
    this.title = title;
    this.edition = edition;
  }
}
```
or
```
@Table
public class Book { ... }
```

### Save Entity
```
Book book = new Book("isbn123", "Title here", "2nd edition")
book.save();
```

### Load Entity
```
Book book = Book.findById(Book.class, 1);
```

### Update Entity
```
Book book = Book.findById(Book.class, 1);
book.title = "updated title here"; // modify the values
book.edition = "3rd edition";
book.save(); // updates the previous entry with new values.
```

### Delete Entity
```
Book book = Book.findById(Book.class, 1);
book.delete();
```

### Update Entity based on Unique values
```
Book book = new Book("isbn123", "Title here", "2nd edition")
book.save();

// Update book with isbn123
Book sameBook = new Book("isbn123", "New Title", "5th edition")
sameBook.update();

book.getId() == sameBook.getId(); // true
```

### Bulk Insert
```
List<Book> books = new ArrayList<>();
books.add(new Book("isbn123", "Title here", "2nd edition"))
books.add(new Book("isbn456", "Title here 2", "3nd edition"))
books.add(new Book("isbn789", "Title here 3", "4nd edition"))
SugarRecord.saveInTx(books);
```

## Contributing

Please fork this repository and contribute back using [pull requests](https://github.com/satyan/sugar/pulls). Features can be requested using [issues](https://github.com/satyan/sugar/issues). All code, comments, and critiques are greatly appreciated.

## Changelog

#### v1.3 [[jar](https://github.com/satyan/sugar/releases/download/v1.3/sugar-1.3.jar)]

- Transaction Support
- Bulk Insert of records 
- Encrypted datastore (branch : sugar-cipher using sqlcipher)
- Removed Constructor with context parameter. Needs default constructor now.
- Enhancements to QueryBuilder
- Bug fixes and other improvements.

#### v1.2 [[jar](https://github.com/satyan/sugar/releases/download/v1.2/sugar-1.2.jar)]

- package restriction for domain classes.
- metadata caching
- QueryBuilder v1
- Database Migrations
- Provision for Raw queries
- Better and more organized api guide and usage instructions.

#### v1.1 [[jar](https://github.com/satyan/sugar/releases/download/v1.1/sugar-1.1.jar)]

- Static api doesn't take context anymore. Hence

```java
Book.findById(context, Book.class, 1);
```

becomes

```java
Book.findById(Book.class, 1);
```

- Some cleanup in the code.
