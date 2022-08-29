
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







