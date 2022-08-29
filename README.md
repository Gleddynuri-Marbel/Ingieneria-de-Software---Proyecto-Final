
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

Estilos de Programacion usados:

1. Programación estructurada (PE)

La programación estructurada esta compuesta por un conjunto de técnicas que han ido evolucionando aumentando considerablemente la productividad del programa reduciendo el tiempo de depuración y mantenimiento del mismo.

Esta programación estructurada utiliza un número limitado de estructuras de control, reduciendo así considerablemente los errores.

Esta técnica incorpora:

Diseño descendente (top-dow): el problema se descompone en etapas o estructuras jerárquicas.
Recursos abstractos (simplicidad): consiste en descompones las acciones complejas en otras más simples capaces de ser resueltas con mayor facilidad.
Estructuras básicas: existen tres tipos de estructuras básicas:
Estructuras secuénciales: cada acción sigue a otra acción secuencialmente. La salida de una acción es la entrada de otra.
Estructuras selectivas: en estas estructuras se evalúan las condiciones y en función del resultado de las mismas se realizan unas acciones u otras. Se utilizan expresiones lógicas.
Estructuras repetitivas: son secuencias de instrucciones que se repiten un número determinado de veces.


2. Programación modular

En la programación modular consta de varias secciones dividas de forma que interactúan a través de llamadas a procedimientos, que integran el programa en su totalidad.

En la programación modular, el programa principal coordina las llamadas a los módulos secundarios y pasa los datos necesarios en forma de parámetros.

A su vez cada modulo puede contener sus propios datos y llamar a otros módulos o funciones.


3. Programación funcional

Se caracteriza principalmente por permitir declarar y llamar a funciones dentro de otras funciones.

## Buenas Practicas - Codigo Legible
**Lenguaje**: <br>
La documentacion, la cual se definiria mas adelante, esta en ingles. Asi para lograr un orden e impecabilidad en el proyecto. <br>
```
    class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True)
    email = db.Column(db.String(100), unique=True)
    password = db.Column(db.String(80))
    institution = db.Column(db.String(100))
    
    
```
```
    class LoginForm(FlaskForm):
    username = StringField('username', validators=[InputRequired(), Length(min=4, max=15)])
    password = PasswordField('password', validators=[InputRequired(), Length(min=8, max=80)])
    remember = BooleanField('remember me')
```
**Documentacion de codigo**: <br>
Cada una de nuestras funciones esta ordenada de tal manera que esta sea facilmente entendida por terceros. A continuacion un fragmento ejemplificando el enunciado anterior. <br>
```
@app.route('/contest', methods=('GET', 'POST'))
def contest():
    title = "Programacion"
    if request.method == 'POST':
      if not request.form['name'] or not request.form['email'] or not request.form['institution'] or not request.form['resume']:
         flash('Llene todos los espacios', 'error')
      else:
         Progra = Program(name=request.form['name'], email=request.form['email'],
            institution=request.form['institution'], resume=request.form['resume'])

         db.session.add(Progra)
         db.session.commit()
         
         flash('Forma enviada')
    return render_template('contest.html', title=title)
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







