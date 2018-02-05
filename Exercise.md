Create a class called Country, and make it look like this: 

```
@Entity
public class Country {
    @Id
    @GeneratedValue(strategy= GenerationType.AUTO)
    private long id;

    @Column(unique=true)
    private String countryname;

    @ManyToMany(mappedBy = "myCountries")
    private List<Person> countryPeople;

    public Country() {
    }

    public Country(String countryname) {
        this.countryname = countryname;
    }

    public long getId() {
        return id;
    }

    public void setId(long id) {
        this.id = id;
    }

    public String getCountryname() {
        return countryname;
    }

    public void setCountryname(String countryname) {
        this.countryname = countryname;
    }

    public List<Person> getCountryPeople() {
        return countryPeople;
    }

    public void setCountryPeople(List<Person> countryPeople) {
        this.countryPeople = countryPeople;
    }
}
```
 
Create a class called Person, and make it look like this: 
```
@Entity
public class Person {
    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private long id;

    private String firstname;

    private String lastname;

    @ManyToMany
    private List<Country> myCountries;

    public Person() {
        myCountries = new ArrayList<>();
    }

    public long getId() {
        return id;
    }

    public void setId(long id) {
        this.id = id;
    }

    public String getFirstname() {
        return firstname;
    }

    public void setFirstname(String firstname) {
        this.firstname = firstname;
    }

    public String getLastname() {
        return lastname;
    }

    public void setLastname(String lastname) {
        this.lastname = lastname;
    }

    public List<Country> getMyCountries() {
        return myCountries;
    }

    public void setMyCountries(List<Country> myCountries) {
        this.myCountries = myCountries;
    }

    public void addCountry(Country c)
    {
        this.myCountries.add(c);
    }
}
```

Make this work, and alter the class to display the details according to the comments below: 

```
@RestController
public class MainController {
    @Autowired
    CountryRepo countryRepo;

    @RequestMapping("/")
    public String addHere()
    {
        Country c = new Country("Ghana");
        countryRepo.save(c);

        c = new Country ("Dominican Republic");
        countryRepo.save(c);

        c = new Country ("United States");
        countryRepo.save(c);

        //List Countries:
        System.out.println("This is a list of countries in the database:");

        for(Country thisCountry:countryRepo.findAll()) {
            System.out.println(thisCountry.getCountryname());
        }

        Person A = new Person();
        A.setFirstname("Jane");
        A.setLastname("Doe");

        A.addCountry(countryRepo.findByCountryname("Ghana"));


        	//Update this exercise:
        /* For each Person in the database, show where they are from. A person can be from more than one country.*/

//Use this section to display a list of people and the countries they are from. 

        return "Check the console for your details";

    }
}
```

