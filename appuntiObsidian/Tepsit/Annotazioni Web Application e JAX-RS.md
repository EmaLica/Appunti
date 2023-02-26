

## Java JAX-RS

JAX-RS è una specifica Java per lo sviluppo di servizi web RESTful. Le annotazioni JAX-RS forniscono un modo per configurare un servizio web RESTful in modo dichiarativo, rendendo più facile e veloce lo sviluppo di applicazioni web.

### Annotazioni

Ecco alcune delle annotazioni JAX-RS più comuni:

1.  @Path: questa annotazione specifica l'URI base per una classe o un metodo del servizio web RESTful. Ad esempio, se si annota una classe con @Path("/hello"), allora il servizio web RESTful associato risponderà alle richieste iniziate con "/hello".

``` java
@Path("/hello")
public class Hello {
}
```

3.  @GET, @POST, @PUT, @DELETE: queste annotazioni specificano il tipo di richiesta HTTP associato al metodo annotato. Ad esempio, se si annota un metodo con @GET, allora il metodo risponderà solo alle richieste GET.

``` java
@GET
@Produces(MediaType.APPLICATION_JSON)
public List<Person> getPersons() {
}

@POST
@Consumes(MediaType.APPLICATION_JSON)
@Produces(MediaType.APPLICATION_JSON)
public Person addPerson(Person person) {
}

@PUT
@Path("/{id}")
@Consumes(MediaType.APPLICATION_JSON)
@Produces(MediaType.APPLICATION_JSON)
public Person updatePerson(@PathParam("id") int id, Person person) {
}

@DELETE
@Path("/{id}")
@Produces(MediaType.APPLICATION_JSON)
public Person deletePerson(@PathParam("id") int id) {
}

```
4.  @Produces, @Consumes: queste annotazioni specificano il tipo di contenuto dei dati che il metodo può produrre o consumare. Ad esempio, se si annota un metodo con @Produces("application/json"), il metodo produrrà solo dati in formato JSON.

``` java
@POST @Path("/add") 
@Consumes(MediaType.APPLICATION_JSON) @Produces(MediaType.APPLICATION_JSON) 
public CalculationResult add(Numbers numbers){
}
```
5.  @PathParam: questa annotazione specifica un parametro di percorso nell'URI. Ad esempio, se si annota un metodo con @Path("/users/{userId}") e @PathParam("userId"), il valore del parametro di percorso verrà passato come argomento al metodo.

``` java

```
6.  @QueryParam: questa annotazione specifica un parametro di query nell'URI. Ad esempio, se si annota un metodo con @Path("/users") e @QueryParam("name"), il valore del parametro di query verrà passato come argomento al metodo.

``` java
@Path("/hello")
public class Hello {

    @GET
    @Produces(MediaType.TEXT_PLAIN)
    public String sayHello() {
        return "Ciao a tutti!";
    }
}
```
7.  @HeaderParam: questa annotazione specifica un parametro di intestazione HTTP. Ad esempio, se si annota un metodo con @HeaderParam("Authorization"), il valore dell'intestazione Authorization verrà passato come argomento al metodo.

``` java
@Path("/hello")
public class Hello {

    @GET
    @Produces(MediaType.TEXT_PLAIN)
    public String sayHello() {
        return "Ciao a tutti!";
    }
}
```
8.  @DefaultValue: questa annotazione specifica un valore predefinito per un parametro. Ad esempio, se si annota un metodo con @QueryParam("name") e @DefaultValue("guest"), il valore predefinito del parametro "name" sarà "guest" se non viene fornito alcun valore.

``` java
@Path("/hello")
public class Hello {

    @GET
    @Produces(MediaType.TEXT_PLAIN)
    public String sayHello() {
        return "Ciao a tutti!";
    }
}
```
- ContextPath: percorso in cui confluiscono i file relativi alla root directory del webserver.

- @ApplicationPath: annotazione che identifica il percorso dell'applicazione che ricopre il ruolo di percorso URL base delle risorse.


- Servlet: componente che consente di gestire l'interazione tra client e server
- ServletContext: componente che si occupa della condivisione di file e dati tra le varie pagine della webapplication.
- @Context: consente di effettuare l'ignezione di richieste e risposte all'interno della webapplication. Lo abbiamo utillizato per inserire il ServletContext utilizzato per lo scambio e accesso di dati e file. 


- @XmlRootElement: annotazione che identifica elementi il cui schema viene scritto in XML.
```java
@XmlRootElement(name = "libro")
public class Libro {
	private String name;
	private String autore;
	...
}
```
```xml
<libro>
	<name>...</name>
	<autore>...</autore>
</libro>
```

- @PathParam: annotazione che consente di estrarre il valore di una variabile all'interno di un percorso.
```java
@Path("/libro/{nomeLibro}")
public String getLibro(@PathParam("nomeLibro") String nomeLibro) {
	return libri.get(nomeLibro);
}
```

- @CookieParam: annotazione che consente di estrarre il valore di una variabile all'interno di un cookie.
```java
@Path("/libro/aggiungi/{nomeLibro}")
public Response addBook(@CookieParam("userToken") String userToken, @PathParam("nomeLibro") String nomeLibro) {
	if (tokens.get(userToken) != null) {
		libri.add(nomeLibro);
		return Response.ok("inserito").status(200).build();
	} else return Response.status(Status.NOT_AUTORIZED).build();
}
```

- @QueryParam: annotazione che consente di estrarre il valore di una variabile all'interno di un percorso URL.
`GET: libri/get?nomeLibro="The Dictator Handbook"`
```java
@GET
public Response readBook(@QueryParam("nomeLibro") String nomeLibro) {
	Libro libro = libri.read(nomeLibro);
	
	return libro != null ? 
	Response.ok(libro).status(200).build() : 
	Response.status(Status.NOT_FOUND).build();	
}
```

- @FormParam: annotazione che consente di estrarre il valore di una variabile all'interno di un form.
```html
<html>
...
<form action="service/login" method="post">
	<input type="text" name="username" placeholder="Username">
	<input type="password" name="password" placeholder="Password">
	<input type="submit" name="login" value="login">
</form>
</html>
```
```java
@GET
public Response login(@FormParam("username") String username, @FormParam("password") String password) {
	User user = new User(username, SHA(password));
	User read = userPersistence.read(user);
	
	if (!user.equals(read)) return Response.status(Status.NOT_AUTORIZED);
	return Response.ok();
}
```

- @Consumes: annotazione che specifica il formato della risposta (corrispettivo dell'header Contet-Type dell'HTTP)
- @Produces: annotazione che specifica il formato della richiesta (corrispettivo  all'header Accept  dell'HTTP)

## Metodi HTTP corrispetivi CRUD: 
- GET: read
- POST: create
- PUT / PATH: update
- DELETE: delete

##  Header HTTP:
contiene i metadati della comunicazione.
Content-Type: 
Accept: 