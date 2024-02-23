## Simple Weather Detector

This project will take an API from https://openweathermap.org/ and detect 
the current weather at the given location. 

The webpage works by taking the input provided by the user on the webpage
and using the API to gather the current weather details of the certain 
city. This data is then converted into json and parsed through.

```cpp
# Create your views here.
def index(request):
    if request.method == "POST":
        city = request.POST['city']
        res = urllib.request.urlopen('https://api.openweathermap.org/data/2.5/weather?q='+city+'&appid=c849b1942911275f098e8da1a4801098').read()
        json_data = json.loads(res)
        data = {
            "country_code": str(json_data['sys']['country']),
            "coordinate": str(json_data['coord']['lon']) + ' ' + str(json_data['coord']['lat']),
            "temp": str(json_data['main']['temp'])+'k',
            "pressure": str(json_data['main']['pressure']),
            "humidity": str(json_data['main']['humidity']),
        }
    else:
        city = ''
        data = {}
    return render(request, 'index.html', {'city': city, 'data': data})
```

## 


