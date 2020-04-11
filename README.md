# Using Paginator in a view function
## Quick Guide
```python
from django.core.paginator import Paginator
from . model import Modelname
from django.shortcuts import render
```

```python
def name_of_view_function(request):
    model_list = Modelname.objects.all()
    paginator = Paginator(model_list, 10) # Show 10 model objects per page.

    page_number = request.GET.get('page')
    page_obj = paginator.get_page(page_number)
    return render(request, 'index.html', {'page_obj': page_obj})
  
```
Remember to Use
| {{page_obj.previous_page_number}} For Previouse Page | {{page_obj.number}} For Current Page 
|-------------|-----------------|
| {{page_obj.next_page_number}} For Next Page | {{page_obj.paginator.num_pages}} For Total Number of Page 
