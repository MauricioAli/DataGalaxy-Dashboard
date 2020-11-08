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

external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

app = dash.Dash(__name__, external_stylesheets=external_stylesheets)

server = app.server

app.layout = html.Div([
    html.H2('Hello World'),
    dcc.Dropdown(
        id='dropdown',
        options=[{'label': i, 'value': i} for i in ['LA', 'NYC', 'MTL']],
        value='LA'
    ),
    html.Div(id='display-value')
])

@app.callback(dash.dependencies.Output('display-value', 'children'),
              [dash.dependencies.Input('dropdown', 'value')])
def display_value(value):
    return 'You have selected "{}"'.format(value)

if __name__ == '__main__':
    app.run_server(debug=True)



```
