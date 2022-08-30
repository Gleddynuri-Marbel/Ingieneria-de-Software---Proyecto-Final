
# Ingieneria-de-Software---Proyecto-Final

Codificacion de la documentacion del presente trabajo.

Integrantes: 
- Alvaro Cano 
- Jenny Huanca
- Gleddynuri Picha

Lenguajes implementados:
-Python
-HTML

Framework:
-Flask

## Propósito del proyecto
Como proposito del trabajo final de nuestro procceding tenemos el  de facilitar el acceso a la información de eventos relacionados a la semana de la computacion dirigido a los estudiantes universitarios. Así como incentivarlos y ayudarlos a su registro e inscripcion en concurso en el que desen participar, ademas de poder programar su horario de asistencia a las charlas de distinguidos ponenetes.


![cs](https://noticias.uneatlantico.es/wp-content/uploads/2017/10/inforuno.jpg)

## Funcionalidades
En primer lugar se tienen wireframes de cada pestaña: Registro, Login, Ponencia, Poster, Programacion Competitiva, los cuales obtienen los datos del usuario que participan en los concursos como de los que no
# Inicio
Dando paso a la presentacion del trabajo final, el inicio se muestra para elegir la opcion que el ususario desee tomar 

### Login
Para login se toma los datos se usuario y del password

### Register
Para esta parte se genera un nuevo usuario con nuevo password que sera parte de la base de datos

### C.Programacion
Realiza el registro para el concurso de programacion competitiva para ser alamacenados en la base de datos 

### Posters
Realiza el registro de nuevos posters para ser alamacenados en la base de datos 

### Logout
Una vez realizado los registros se puede dar la opcion de salir con logout



## Estilos de Programación aplicados;
1. CODE-GOLF

Tan pocas líneas de código como sea posible

```
@app.route('/')
def index():
    title = "Inicio"
    return render_template('index.html', title=title)

```
2. PIPELINE

Problema mayor descompuesto en abstracciones funcionales. Las funciones, según las Matemáticas, son relaciones de entradas a salidas.
Problema más grande resuelto como una canalización de aplicaciones de funciones

```
@app.route('/download/<upload_id>')
def download(upload_id):
    Posterm = Poster_C.query.filter_by(id=upload_id).first()
    return send_file(BytesIO(Posterm.data), attachment_filename=Posterm.filename, as_attachment=True)
```



3. COOKBOOK
Problema más grande descompuesto en abstracciones de procedimiento
Problema más grande resuelto como una secuencia de comandos, cada uno correspondiente a un procedimiento

```
@app.route('/register', methods=['GET', 'POST'])
def register():
    form = RegisterForm()

    if form.validate_on_submit():
        hashed_password = generate_password_hash(form.password.data, method='sha256')
        new_user = User(username=form.username.data, email=form.email.data, institution=form.institution.data, password=hashed_password)
        db.session.add(new_user)
        db.session.commit()

        return '<h1>Nuevo usuario registrado</h1>'

    return render_template('register.html', form=form)
```

## Buenas Practicas - Codigo Legible
**Lenguaje**: <br>
La documentacion, la cual se definiria mas adelante, esta en ingles. Asi para lograr un orden e impecabilidad en el proyecto. <br>
```
class Program(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50))
    email = db.Column(db.String(100), unique=True)
    institution = db.Column(db.String(100))
    resume = db.Column(db.String(260))
    
    
```
```
    class RegisterForm(FlaskForm):
    email = StringField('email', validators=[InputRequired(), Email(message='Invalid email'), Length(max=50)])
    username = StringField('username', validators=[InputRequired(), Length(min=4, max=15)])
    password = PasswordField('password', validators=[InputRequired(), Length(min=8, max=80)])
    institution = StringField('institution', validators=[InputRequired(), Length(max=80)])
```
**Documentacion de codigo**: <br>
Cada una de nuestras funciones esta ordenada de tal manera que esta sea facilmente entendida por terceros. A continuacion un fragmento ejemplificando el enunciado anterior. <br>
```
@app.route('/register', methods=['GET', 'POST'])
def register():
    form = RegisterForm()

    if form.validate_on_submit():
        hashed_password = generate_password_hash(form.password.data, method='sha256')
        new_user = User(username=form.username.data, email=form.email.data, institution=form.institution.data, password=hashed_password)
        db.session.add(new_user)
        db.session.commit()

        return '<h1>Nuevo usuario registrado</h1>'

    return render_template('register.html', form=form)
```
**Modularidad**: <br>
Cada fragmento del codigo ejerce una sola funcion; teniendo el cuenta que utilizamos el framework de Flask, la modularidad y flexibilidad es necesaria. Todo ello permite tambien a la resolucion de errores de forma sencilla, sin comprometer la integridad del resto del proyecto. <br>
```
{% extends "bootstrap/base.html" %}
{% import "bootstrap/wtf.html" as wtf %}

{% block title %}
Login
{% endblock %}

{% block styles %}
{{super()}}
<link rel="stylesheet" href="{{ url_for('static',filename='css/style_02.css') }}">
{% endblock %}

{% block content %}
    <div class="container">

      <form class="form-signin" method="POST" action="/login">
        <h2 class="form-signin-heading">Login</h2>
        {{ form.hidden_tag() }}
        {{ wtf.form_field(form.username) }}
        {{ wtf.form_field(form.password) }}
        {{ wtf.form_field(form.remember) }}
        <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
      </form>

    </div> <!-- /container -->
{% endblock %}
```
**Indentacion Consistente**: <br>
Vale la pena señalar que es una buena idea mantener un estilo de indentacion consistente.
Hay más de una forma de indentar el código.

```
@app.route('/register', methods=['GET', 'POST'])
def register():
    form = RegisterForm()

    if form.validate_on_submit():
        hashed_password = generate_password_hash(form.password.data, method='sha256')
        new_user = User(username=form.username.data, email=form.email.data, institution=form.institution.data, password=hashed_password)
        db.session.add(new_user)
        db.session.commit()

        return '<h1>Nuevo usuario registrado</h1>'

    return render_template('register.html', form=form)
```
**Evite los comentarios obvios**: <br>
Comentar el código es fantástico; sin embargo, puede ser exagerado o simplemente redundante. Toma este ejemplo:

```
@app.route('/contest', methods=('GET', 'POST'))
def contest():
    title = "Programacion"
    if request.method == 'POST':
      if not request.form['name'] or not request.form['email'] or not request.form['institution'] or not request.form['resume']: #Si no se encuentra una casilla que el proceso se detenga
         flash('Llene todos los espacios', 'error')
      else:
         Progra = Program(name=request.form['name'], email=request.form['email'], #Se insertan los valores segun el form
            institution=request.form['institution'], resume=request.form['resume'])

         db.session.add(Progra) #Se ejecuta la variable insertando la data
         db.session.commit()
         
         flash('Forma enviada')
    return render_template('contest.html', title=title)
```

# SOLID

## 1. S-Principio de Resposabilidad Única:
  Este principio tiene como objetivo separar los comportamientos para que, si surgen errores como resultado de su cambio, no         afecten otros comportamientos no relacionados.
```
@app.route('/download/<upload_id>')
def download(upload_id):
    Posterm = Poster_C.query.filter_by(id=upload_id).first()
    return send_file(BytesIO(Posterm.data), attachment_filename=Posterm.filename, as_attachment=True)

@app.route('/ponent')
def ponent():
    title = "Ponentes"
    return render_template('ponent.html', title=title)

@app.route('/logout')
@login_required
def logout():
    logout_user()
    return redirect(url_for('index'))
```
**Formato**: <br>
El codigo en su totalidad esta ordenado y formateado en funcion que sea legible. <br>

![Open_Closed](https://github.com/ThatGust/Ingieneria-de-Software---Proyecto-Final/blob/main/image_2022-08-29_141629603.png)
## 2. O-Principio de Abierto-Cerrado:
  Este principio tiene como objetivo extender el comportamiento de una Clase sin cambiar el comportamiento existente de esa Clase.   Esto es para evitar causar errores dondequiera que se use la Clase.
  Para aplicar este ejemplo todas  las clases deben descender de una clase abstracta donde se presenten todos aquellos métodos que   son la base de las respectivas clases.
```
{% extends "layout_2.html" %}
{% import "bootstrap/wtf.html" as wtf %}
{% block head %}
{{ super() }}
{% endblock %}
{% block title %}{{title}}{% endblock %}
```
## 3. L - Sustitución de Liskov:
  Este principio tiene como objetivo hacer cumplir la coherencia para que la Clase principal o su Clase secundaria se puedan     usar de la misma manera sin errores.
  Para aplicar este ejemplo todas  las clases que sean subtipos de una superclase , y esta misma debe incluir solo aquellos       métodos que comparten ambas subclases sin romper la lógica.
```
Layouts
```
![Open_Closed](https://github.com/ThatGust/Ingieneria-de-Software---Proyecto-Final/blob/main/Capture.PNG)






