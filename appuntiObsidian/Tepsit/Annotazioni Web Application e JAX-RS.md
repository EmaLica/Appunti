
## Metodi HTTP corrispetivi CRUD: 
- GET: read
- POST: create
- PUT / PATH: update
- DELETE: delete

##  Header HTTP:
contiene i metadati della comunicazione.
Content-Type: 
Accept: 

## Specifiche Java
- Glassfish: applicazione Java EE che supporta lo sviluppo di Jakarta REST API
- ContextPath: percorso in cui confluiscono i file relativi alla root directory del webserver.

- @ApplicationPath: annotazione che identifica il percorso dell'applicazione che ricopre il ruolo di percorso URL base delle risorse.

- @Path: annotazione che identifica il percorso con cui una classe o metodo rispondono alle richieste.

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
