# Save data in a local database using Room

- Apps that handle non-trivial amounts of structured data can benefit greatly from persisting that data locally.
- when the internet go down we using hte cache.
- The Room persistence library provides an abstraction layer over SQLite to allow fluent database access while harnessing the full power of SQLite.

***Room provides the following benefits:***

1. Compile-time verification of SQL queries.
2. Convenience annotations that minimize repetitive and error-prone boilerplate code.
3. Streamlined database migration paths.

**To use room we add the following dependencies:**

```
dependencies {
    def room_version = "2.3.0"

    implementation "androidx.room:room-runtime:$room_version"
    annotationProcessor "androidx.room:room-compiler:$room_version"

    // optional - RxJava2 support for Room
    implementation "androidx.room:room-rxjava2:$room_version"

    // optional - RxJava3 support for Room
    implementation "androidx.room:room-rxjava3:$room_version"

    // optional - Guava support for Room, including Optional and ListenableFuture
    implementation "androidx.room:room-guava:$room_version"

    // optional - Test helpers
    testImplementation "androidx.room:room-testing:$room_version"

    // optional - Paging 3 Integration
    implementation "androidx.room:room-paging:2.4.0-alpha04"
}
```

***There are three major components in Room:***

1. The database class that holds the database and serves as the main access point for the underlying connection to your app's persisted data.
2. Data entities that represent tables in your app's database.
3. Data access objects (DAOs) that provide methods that your app can use to query, update, insert, and delete data in the database.

***Data entity***

- we use @Entity for the class .
- we use @PrimaryKey for the id .
- @ColumnInfo for the column name.

***Data access object (DAO)***

- its interface .
- the interface notate with @Dao
- we add into it our methods and queries .

***Database***

- The database class must satisfy the following conditions:

1. The class must be annotated with a @Database annotation that includes an entities array that lists all of the data entities associated with the database.
2. The class must be an abstract class that extends RoomDatabase.
3. For each DAO class that is associated with the database, the database class must define an abstract method that has zero arguments and returns an instance of the DAO class.

***Usage***

- to create an instance of the database:

```
AppDatabase db = Room.databaseBuilder(getApplicationContext(),
        AppDatabase.class, "database-name").build();
```

- you can use the methods from the DAO instance to interact with the database:

```
UserDao userDao = db.userDao();
List<User> users = userDao.getAll();
```

***Define a composite primary key***

- by using the primary key in the entity of class .

```
@Entity(primaryKeys = {"firstName", "lastName"})
public class User {
    public String firstName;
    public String lastName;
}
```

***@Ignore***

- If an entity has fields that you don't want to persist, you can annotate them using @Ignore.
- In cases where an entity inherits fields from a parent entity, it's usually easier to use the ignoredColumns property of the @Entity attribute:

```
@Entity(ignoredColumns = "picture")
public class RemoteUser extends User {
    @PrimaryKey
    public int id;

    public boolean hasVpn;
}
```

- If your app requires very quick access to database information through full-text search (FTS) we can annotate it with  @Fts3 or @Fts4 .

- In cases where a table supports content in multiple languages, use the languageId option to specify the column that stores language information for each row:

```
@Fts4(languageId = "lid")
```

***Index specific columns***

- If your app must support SDK versions that don't allow for using FTS3- or FTS4-table-backed entities, you can still index certain columns in the database to speed up your queries.

```
@Entity(indices = {@Index("name"),
        @Index(value = {"last_name", "address"})})
```

- You can enforce this uniqueness property by setting the unique property of an @Index annotation to true.

```
@Entity(indices = {@Index(value = {"first_name", "last_name"},
        unique = true)})
```

***Include AutoValue-based objects***

- When using classes annotated with @AutoValue as entities, you can annotate the class's abstract methods using @PrimaryKey, @ColumnInfo, @Embedded, and @Relation.
- When using these annotations, however, you must include the @CopyAnnotations annotation each time so that Room can interpret the methods' auto-generated implementations properly.

```
@AutoValue
@Entity
public abstract class User {
    // Supported annotations must include `@CopyAnnotations`.
    @CopyAnnotations
    @PrimaryKey
    public abstract long getId();

    public abstract String getFirstName();
    public abstract String getLastName();

    // Room uses this factory method to create User objects.
    public static User create(long id, String firstName, String lastName) {
        return new AutoValue_User(id, firstName, lastName);
    }
}
```

## Define relationships between objects

- To store the composed columns separately in the table, include an Address class field in the User class that is annotated with @Embedded .

```
public class Address {
    public String street;
    public String state;
    public String city;

    @ColumnInfo(name = "post_code") public int postCode;
}

@Entity
public class User {
    @PrimaryKey public int id;

    public String firstName;

    @Embedded public Address address;
}
```

***Define one-to-one relationships***

- we connect two entity's by  reference to the primary key of the other entity.

```
@Entity
public class User {
    @PrimaryKey public long userId;
    public String name;
    public int age;
}

@Entity
public class Library {
    @PrimaryKey public long libraryId;
    public long userOwnerId;
}
```

- the relationship notate :

```
public class UserAndLibrary {
    @Embedded public User user;
    @Relation(
         parentColumn = "userId",
         entityColumn = "userOwnerId"
    )
    public Library library;
}
```

- Finally, add a method to the DAO class that returns all instances of the data class that pairs the parent entity and the child entity.
- This method requires Room to run two queries, so add the @Transaction annotation to this method to ensure that the whole operation is performed atomically.

```
@Transaction
@Query("SELECT * FROM User")
public List<UserAndLibrary> getUsersAndLibraries();
```

***one-to-many relationships***

- same one to one  first link to entity's with a reference id to the outer entity ,second add the relation between the two ,and third add it to DAO class .

***many-to-many relationships***

- same the one to many but hte relation different :

```
 @Relation(
         parentColumn = "playlistId",
         entityColumn = "songId",
         associateBy = @Junction(PlaylistSongCrossref.class)
    )
    public List<Song> songs;
```

- and for the DAO class we need to add to two Query to get each list .

## Accessing data using Room DAOs

- There are two types of DAO methods that define database interactions:

1. Convenience methods that let you insert, update, and delete rows in your database without writing any SQL code.
2. Query methods that let you write your own SQL query to interact with the database.

***Convenience methods***

1. Insert

- The @Insert annotation allows you to define methods that insert their parameters into the appropriate table in the database.

2. Update

- The @Update annotation allows you to define methods that update specific rows in a database table.
- Similarly to @Insert methods, @Update methods accept data entity instances as parameters.

3. Delete

- The @Delete annotation allows you to define methods that delete specific rows from a database table.
- Similarly to @Insert methods, @Delete methods accept data entity instances as parameters.

***Query methods***

1. Simple queries

```
@Query("SELECT * FROM user")
public User[] loadAllUsers();
```

- we can return specific column  from a database :

```
@Query("SELECT first_name, last_name FROM user")
public List<NameTuple> loadFullName();
```

2. Pass simple parameters to a query

```
@Query("SELECT * FROM user WHERE age > :minAge")
public User[] loadAllUsersOlderThan(int minAge);
```

- You can also pass multiple parameters or reference the same parameter multiple times in a query.

```
@Query("SELECT * FROM user WHERE age BETWEEN :minAge AND :maxAge")
public User[] loadAllUsersBetweenAges(int minAge, int maxAge);

@Query("SELECT * FROM user WHERE first_name LIKE :search " +
       "OR last_name LIKE :search")
public List<User> findUserWithName(String search);
```

3. Pass a collection of parameters to a query

```
@Query("SELECT * FROM user WHERE region IN (:regions)")
public List<User> loadUsersFromRegions(List<String> regions);
```

4. Query multiple tables

```
@Query("SELECT * FROM book " +
       "INNER JOIN loan ON loan.book_id = book.id " +
       "INNER JOIN user ON user.id = loan.user_id " +
       "WHERE user.name LIKE :userName")
public List<Book> findBooksBorrowedByNameSync(String userName);
```

- You can also define simple objects to return a subset of columns from multiple joined tables as discussed in Return a subset of a table's columns.

```
  @Query("SELECT user.name AS userName, book.name AS bookName " +
          "FROM user, book " +
          "WHERE user.id = book.user_id")
   public LiveData<List<UserBook>> loadUserAndBookNames();
```

***Special return types***

- Room provides some special return types for integration with other API libraries :

1. Paginated queries with the Paging library

- Room supports paginated queries through integration with the Paging library. In Room 2.3.0-alpha01 and higher, DAOs can return PagingSource objects for use with Paging 3.

```
@Dao
interface UserDao {
  @Query("SELECT * FROM users WHERE label LIKE :query")
  PagingSource<Integer, User> pagingSource(String query);
}
```

2. Direct cursor access

- If your app's logic requires direct access to the return rows, you can write your DAO methods to return a Cursor object.

```
@Dao
public interface UserDao {
    @Query("SELECT * FROM user WHERE age > :minAge LIMIT 5")
    public Cursor loadRawUsersOlderThan(int minAge);
}
```
