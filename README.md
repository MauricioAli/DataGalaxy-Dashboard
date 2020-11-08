# DataGalaxy-Dashboard

Saludos este es un paso a paso de como crear tu primer dashboad con dash ploty ,importar diferetes graficas y poder compartirlo con ngrok o mejor aun por heroku.


# Que es Dash?

Dash es un Framework productivo de Python para crear aplicaciones de análisis web.

Escrito sobre Flask, Plotly.js y React.js, Dash es ideal para crear aplicaciones de visualización de datos con interfaces de usuario altamente personalizadas en Python puro. Es especialmente adecuado para cualquiera que trabaje con datos en Python.

# Documentación oficial

https://dash.plotly.com/

# Mi primer app

```python

import os
import dash
import dash_core_components as dcc
import dash_html_components as html
import plotly.express as px
import plotly.graph_objs as go
import dash_daq as daq
import dash_bootstrap_components as dbc


external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']


app = dash.Dash(__name__, external_stylesheets=[dbc.themes.BOOTSTRAP])

server = app.server


df = px.data.iris()
fig= px.scatter(df,x="sepal_width",y="sepal_length")
grafica_1= dcc.Graph(figure=fig)


fig2 = go.Figure(data=[go.Scatter(x=[1,2,3,4],y=[1,2,3,4])])
grafica_2=dcc.Graph(figure=fig2)


grafica_3=dcc.Graph(
        id='example-graph',
        figure={
            'data': [
                {'x': [1, 2, 3], 'y': [4, 1, 2], 'type': 'bar', 'name': 'SF'},
                {'x': [1, 2, 3], 'y': [2, 4, 5], 'type': 'bar', 'name': u'Montréal'},
            ],
            'layout': {
                'title': 'Dash Data Visualization'
            }
        }
    )



indicador_1=daq.Knob(

            size=400,
            max=10,
            color={"ranges":{"green":[0,5],"yellow":[5,9],"red":[9,10]}}


)


body = html.Div(
    [
        
        dbc.Row(
            [
                dbc.Col(grafica_1),
                dbc.Col(grafica_2),
                dbc.Col(grafica_3),
            ]
        ),
        dbc.Row(dbc.Col(indicador_1),),
    ]
)



app.layout=html.Div([ 
body
])

if __name__ == '__main__':
    app.run_server(debug=True)



```

# Compartir usando ngrok 
 Un comando para crear una URL instantánea y segura a su servidor localhost a través de cualquier NAT o firewall.
 Documentacion oficial
 https://ngrok.com/
 
 para descargar https://ngrok.com/download y siga las instrucciones 
 
 teniendo el servidor ejecutando de dash abrimos una nueva terminal y ejecutamos ./ngrok http [puerto de nuestro proyecto]
 
 # Deploy usando heroku
 
 Debemos tener nuestro proyecto en un entorno virtual en la carpea del proyecto.
```
$ git init       
$ virtualenv venv 
$ source venv/bin/activate 

```
Instalamos el servidor http para flask

```
pip install gunicorn
```
El nombre de nuestro alchivo python debe ser app.py y ahora tenemos que crear 3 archivos:

.gitignore
```
venv
*.pyc
.DS_Store
.env

```
Profile
```
web: gunicorn app:server --log-file=-

```

requirements.txt
```
pip freeze > requirements.txt
```

Necesitamos tener una cuenta heroku https://id.heroku.com/login e installar heroku cli https://devcenter.heroku.com/articles/heroku-cli#download-and-install

Creamos nuestro proyecto heroku y procedemos a hacer push al servidor de heroku. 
```
$ heroku create my-dash-app 

$ git add . 
$ git commit -m 'primer Deploy'
$ heroku git:remote -a my-dash-app
$ git push heroku master 

```
Esperamos que termine todo el proceso y ya podemos entrar al link resultante.
https://dashapp22.herokuapp.com/

# Eso es todo, espero ver sus propios dashboard 

