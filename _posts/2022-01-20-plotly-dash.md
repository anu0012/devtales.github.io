---
layout: post
title: Creating Interactive Dashboards using Plotly Dash
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Python, Plotly, Dash, Visualization, Tools and Libraries]
---

Dash is an open-source python library which is used for building interactive web-based applications. It is a powerful tool that can be used for building reporting dashboards.

### Why you should try it

1. It is free and open source unlike other popular BI tools like Tableau or Microsoft PowerBI.

2. If you handle your data in python and looking for a data visualization library.

3. It is written on top of Flask, Plotly.js and React.js which allows you to easily deploy your flask based web server on AWS or Azure and you can create customizable and reusable components.

4. It provides very cool and appealing plots and charts which are both cross-platform and mobile supported.

5. It requires only Python and some basic knowledge of HTML to start with. No Javascript/d3.js is required for building dashboards.

### Installation

We need to install several packages as following - 
```
pip install Flask
pip install dash
pip install plotly
pip install dash_html_components
pip install dash_core_components
```

### Dashboard

Let's start discussing about different components of Dash and then we'll build our first dashboard.

Dash divides its components into two categories - 

1. `Dash HTML Components` - This part helps us to create HTML elements inside our application. It supports varity of HTML tags.

```
import dash_html_components as html

html.Div([
    html.H1('Hello Dash'),
    html.Div([
        html.P('This is a paragraph.')
    ])
])
```

This python structure will be converted into HTML elements.

2. `Dash Core Components` - This part gives interactive elements to our dashboard like dropdown, sliders, datepickers etc. Let's see an example.

```
import dash_core_components as dcc

dcc.Dropdown(
    options=[
        {'label': 'United States of America', 'value': 'USA'},
        {'label': 'India', 'value': 'IND'},
        {'label': 'Japan', 'value': 'JPN'}
    ],
    value='IND'
)  
```

Now let's build a sample application. For the dashboard, we can read the data simply by pandas or create our own data. 

1. First we need to import all dependencies.

```
import dash
import dash_core_components as dcc
import dash_html_components as html
import plotly.express as px
import pandas as pd
```

2. We need to instantiate Dash object.

`app = dash.Dash(__name__)`

3. Let's create some dummy data for our dashboard.

```
df = pd.DataFrame({
    "Indicator": ["Total Cases", "Recovered", "Total Cases", "Recovered"],
    "Cases": [19111326, 11219123, 10147468, 9717834],
    "Country": ["USA", "USA", "India", "India"]
})
```

4. Now let's create a bar plot.

`fig = px.bar(df, x="Indicator", y="Cases", color="Country", barmode="group")`

5. To add this bar plot to our dashboard we will create a Graph component and put this figure inside it.

```
dcc.Graph(
        id='example-graph-2',
        figure=fig
    )
```

This Graph component will come inside our `app.layout`. This `layout` contains tree of components like `html.Div` and `dcc.Graph`. We can put nested HTML components inside our layout and create more complex ones. This is how our final codebase will look like.

```
import dash
import dash_core_components as dcc
import dash_html_components as html
import plotly.express as px
import pandas as pd

app = dash.Dash(__name__)

df = pd.DataFrame({
    "Indicator": ["Total Cases", "Recovered", "Total Cases", "Recovered"],
    "Cases": [19111326, 11219123, 10147468, 9717834],
    "Country": ["USA", "USA", "India", "India"]
})

fig = px.bar(df, x="Indicator", y="Cases", color="Country", barmode="group")

app.layout = html.Div(style={'backgroundColor': '#111111'}, children=[
    html.H1(
        children='Hello Dash',
        style={
            'textAlign': 'center',
            'color': '#7FDBFF'
        }
    ),

    html.Div(children='Dash: Python based web framework for interactive data visualization.', style={
        'textAlign': 'center',
        'color': '#7FDBFF'
    }),

    dcc.Graph(
        id='example-graph-2',
        figure=fig
    )
])

if __name__ == '__main__':
    app.run_server(debug=True)
```

You can save this as `index.py` and run it using `python index.py` inside terminal. This is how it will look like - 

[Dashboard Image](https://www.dropbox.com/s/yspeay7vypseb6y/Screenshot%202020-12-25%20at%205.36.37%20PM.png?dl=0)

### Callbacks

Callbacks are functions which are called when a particular event occurs. Suppose we select a dropdown item, and we want our graph to be updated accordingly. In such cases, we can use callbacks. In dash, for callbacks we use `app.callback` decorator. 

```
@app.callback(
    Output(component_id='my-output', component_property='children'),
    Input(component_id='my-input', component_property='value')
)
def update_figure(input_params):
	### code for callback function
```

Let's see an example.

```
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
import plotly.express as px

import pandas as pd

df = pd.read_csv('https://covidtracking.com/data/download/national-history.csv')
df['month'] = pd.to_datetime(df['date']).dt.month
df = df.groupby(by=['month']).agg(sum).reset_index(drop=False)

app = dash.Dash(__name__)

app.layout = html.Div([
    dcc.Graph(id='graph-with-slider'),
    dcc.Slider(
        id='month-slider',
        min=df['month'].min(),
        max=df['month'].max(),
        value=df['month'].min(),
        marks={str(month): str(month) for month in df['month'].unique()},
        step=None
    )
])


@app.callback(
    Output('graph-with-slider', 'figure'),
    [Input('month-slider', 'value')])
def update_figure(selected_month):
    filtered_df = df[df.month == selected_month]

    fig = px.bar(filtered_df, x="month", y="positive", hover_name="month",
                     log_x=True)

    fig.update_layout(transition_duration=500)

    return fig


if __name__ == '__main__':
    app.run_server(debug=True)
```

This will create a slider. On changing the slider values, a callback will be generated which will change the plot values. 

[Callback Example](https://www.dropbox.com/s/8o7r8dyy3bliyiu/Screenshot%202020-12-25%20at%206.17.08%20PM.png?dl=0)

So far you must have understood how exactly plotly works. Now let's build another dashboard. We'll be using [this dataset](https://archive.ics.uci.edu/ml/datasets/Bank%2BMarketing) from UCI Machine learning repository.

```
import dash
import dash_table
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
import plotly.express as px
import seaborn as sns

import pandas as pd

df = pd.read_csv('bank.csv')
#print(df.head())
app = dash.Dash(__name__)

fig1 = px.scatter(df, x="age", y="balance", color="job",
                 #size="duration", color="deposit", hover_name="job",
                 log_x=True, size_max=60)

vals = df['marital'].value_counts().tolist()
labels = ['married', 'divorced', 'single']

fig2 = px.bar(x=labels, y=vals)

fig3 = px.pie(df, "deposit", color="deposit")

fig4 = px.imshow(df.corr())

fig5 = px.histogram(df, x="age", y="duration", color="loan",
                   marginal="box", # or violin, rug
                   hover_data=df.columns)

app.layout = html.Div([
    dcc.Graph(
        id='bubble',
        figure=fig1
    ),
    dcc.Graph(
        id='bar',
        figure=fig2
    ),
    dcc.Graph(
        id='pie',
        figure=fig3
    ),
    dcc.Graph(
        id='correlation_matrix',
        figure=fig4
    ),
    dcc.Graph(
        id='histogram',
        figure=fig5
    ),
    dash_table.DataTable(
        id='table',
        columns=[{"name": i, "id": i} for i in df.columns],
        data=df.head(20).to_dict('records'),
    )
])

if __name__ == '__main__':
    app.run_server(host='0.0.0.0', port=8000,debug=True)
```

Below are some of the screenshots of our dashboard:

[1](https://www.dropbox.com/s/pbkknbe5pjkp0qp/1.png?dl=0)

[2](https://www.dropbox.com/s/0uq63eppzrhg48g/2.png?dl=0)

[3](https://www.dropbox.com/s/t3ted2aitcjj7d2/3.png?dl=0)

[4](https://www.dropbox.com/s/ubb0bl1tzzanbf5/4.png?dl=0)

[5](https://www.dropbox.com/s/69n5gd54pwj0sht/5.png?dl=0)

### Deployment to cloud

Dash Enterprise provides the facility to deploy our dash apps on cloud based platforms like AWS, Azure or GCP. Dash Enterprise provides varity of features including Job Queue, Password Vault, Kubernates, Reporting and User Analytics. It ensures the safety of our application and keeps our application private to our organisation. If you want to deploy it on public platform, you can try Heroku. You can try this [link](https://dash.plotly.com/deployment) for more details.

That's all for now. Now it's your turn to try this awesome library. Happy coding :)