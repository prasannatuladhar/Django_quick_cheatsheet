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


```html
<nav aria-label="...">
  <ul class="pagination justify-content-center">
    <li class="page-item ">
      <a class="page-link" href="?page=1" tabindex="-1">&laquo;</a>
    </li>
    {% if page_obj.has_previous %}
      <li class="page-item"><a class="page-link" href="?page={{page_obj.previous_page_number}}">{{page_obj.previous_page_number}}</a></li>
    {% endif %}
    <li class="page-item active">
      <a class="page-link" href="?page={{page_obj.number}}">{{page_obj.number}} <span class="sr-only">(current)</span></a>
    </li>
    {% if page_obj.has_next %}
      <li class="page-item"><a class="page-link" href="?page={{page_obj.next_page_number}}">{{page_obj.next_page_number}}</a></li>
    {% endif %}
    <li class="page-item">
      <a class="page-link" href="?page={{page_obj.paginator.num_pages}}">&raquo;</a>
    </li>
  </ul>
</nav>
  
```
