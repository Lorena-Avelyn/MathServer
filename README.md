# Ex.05 Design a Website for Server Side Processing
## Date:04/12/2024

## AIM:
 To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side. 


## FORMULA:
P = I<sup>2</sup>R
<br> P --> Power (in watts)
<br> I --> Intensity
<br> R --> Resistance

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

## PROGRAM :
math.html
```<!DOCTYPE html>
<html>
    <head>
        <style>
            body{
                margin-top: 20%;
                font-weight: bold;
            }
        </style>
        <script>
            function power()
            {
                const i=document.getElementById("in").value;
                const r=document.getElementById("resistance").value;
                const p= i*i*r; 
                document.getElementById("Answer").innerText="Power :"+ p;
            }
        </script>
    </head>
        <body bgcolor="E6E6FA">
            <center>
                <input type="number" placeholder="Enter Value of Intensity" id="in"><br><br>
                <input type="number" placeholder="Enter Value of Resistance" id="resistance"><br><br>
                <input type="button" onclick="power()" value="Calculate Power"><br><br>
                <label id="Answer"></label>
            </center>
        </body>
</html>
```
views.py
```
from django.shortcuts import render

def calculate_power(request):
    print("calculate_power view called")
    context = {
        'power': "0",
        'current': "0",
        'resistance': "0"
    }
    if request.method == 'POST':
        print("POST request received")
        try:
            current = float(request.POST.get('current', 0))
            resistance = float(request.POST.get('resistance', 0))
            context['power'] = round(current**2 * resistance, 2)
            context['current'] = current
            context['resistance'] = resistance
        except ValueError:
            context['power'] = "Invalid input"
    return render(request, 'mathapp/math.html', context)
```
urls.py
```
from django.contrib import admin
from django.urls import path
from mathapp import views
urlpatterns = [
    path('admin/', admin.site.urls),
    path('powercalc/', views.calculate_power, name="powercalc"),
    path('', views.calculate_power, name="powercalcroot"),
]
```

## SERVER SIDE PROCESSING:
![alt text](<Screenshot 2024-12-04 231917.png>)

## HOMEPAGE:
![alt text](<Screenshot 2024-12-04 231548.png>)

## RESULT:
The program for performing server side processing is completed successfully.
