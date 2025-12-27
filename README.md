# Ex.04 Design a Website for Server Side Processing
## Date:20.12.25

## AIM:
To create a web page to calculate vehicle mileage and fuel efficiency using server-side scripts.

## FORMULA:
M = D / F
<br> M --> Mileage (in km/l)
<br> D --> Distance Travelled (in km)
<br> F --> Fuel Consumed (in l)

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create python programs for views and urls to perform server side processing.

### Step 5:
Create a HTML file to implement form based input and output.

### Step 6:
Publish the website in the given URL.

## PROGRAM:
```
math.html

<!DOCTYPE html>
<html>
<head>
    <title>Power Calculator</title>
    <style>
        body {
    background-color: red;
    font-family: Arial, sans-serif;
    text-align: center;
}

.container {
    background-color: blue;
    border: 5px dashed green;
    width: 400px;
    padding: 30px;
    margin: 100px auto;
    color: white;
    border-radius: 10px;
}

h1 {
    color: pink;
}

input[type="text"] {
    width: 100px;
    padding: 5px;
    margin-left: 10px;
}

input[type="submit"] {
    padding: 5px 15px;
    background-color: white;
    border: none;
    cursor: pointer;
    font-weight: bold;
}

input[type="submit"]:hover {
    background-color: lightgray;
}

    </style>
</head>
<body>
    <h1>Incandescent Bulb Power Calculator</h1>

    <form method="post">
        {% csrf_token %}
        <label for="current">Current (I) in Amps:</label>
        <input type="text" id="current" name="current" required><br><br>

        <label for="resistance">Resistance (R) in Ohms:</label>
        <input type="text" id="resistance" name="resistance" required><br><br>

        <input type="submit" value="Calculate Power">
    </form>

    {% if result is not None %}
        <h2>Power (P) = {{ result }} Watts</h2>
    {% endif %}

    {% if error %}
        <p style="color: red;">{{ error }}</p>
    {% endif %}
</body>
</html>


views.py 

from django.shortcuts import render

def calculate_power(request):
    result = None
    error = None

    if request.method == 'POST':
        try:
            current = float(request.POST.get('current'))
            resistance = float(request.POST.get('resistance'))
            power = (current ** 2) * resistance
            result = round(power, 2)
        except (ValueError, TypeError):
            error = "Invalid input. Please enter valid numbers."

    return render(request, 'mathapp/math.html', {'result': result, 'error': error})



mathapp/urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('', views.calculate_power, name='calculate_power'),
]



mathproject/urls.py

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('mathapp.urls')),
]
```


## OUTPUT - SERVER SIDE:

<img width="1057" height="616" alt="image" src="https://github.com/user-attachments/assets/2690978c-390a-429c-842b-b2653cf4b757" />



## OUTPUT - WEBPAGE:


<img width="1084" height="588" alt="image" src="https://github.com/user-attachments/assets/898aa11c-6e77-464f-b54b-e8ac989aa49b" />

## RESULT:
The a web page to calculate vehicle mileage and fuel efficiency using server-side scripts is created successfully.
