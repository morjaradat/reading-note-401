# Many to many relationships

- its type of relationship is determined by each other (its has many thing depend on many other thing).

- first  annotated both with @Manytomany .
- one of them will take mappedBy some name and will take a HashSet that type of  other class ,like:

```
@Entity
@Table(name = "Project")
public class Project {    
    // ...  
 
    @ManyToMany(mappedBy = "projects")
    private Set<Employee> employees = new HashSet<>();

}
```

- the other one will take cascade = { CascadeType.ALL } and will take a HashSet that type of  other class and will take a the join table annotated that have a table name ,joinColumns with colum name and inverseJoinColumns with name ,like :

```
@Entity
@Table(name = "Employee")
public class Employee { 

    @ManyToMany(cascade = { CascadeType.ALL })
    @JoinTable(
        name = "Employee_Project", 
        joinColumns = { @JoinColumn(name = "employee_id") }, 
        inverseJoinColumns = { @JoinColumn(name = "project_id") }
    )

    Set<Project> projects = new HashSet<>();
}
```
