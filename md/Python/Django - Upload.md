
##Django - Upload

###url.py
```python
 ```
```python
 ```
upload.py
```python
 from django import newforms as forms  
 from django.shortcuts import render_to_response  
 from pagechat.settings import MEDIA_ROOT  
 
 class SimpleFileForm(forms.Form):  
 	file = forms.Field(widget=forms.FileInput, required=False)  
 
 
 def directupload(request):  
 	template = 'fileupload.html'  
 
 	if len(request.FILES) != 0:  
 		if 'file' in request.FILES:  
 			file = request.FILES['file']  
 
 			# Other data on the request.FILES dictionary - add restriction for real usage HERE!
 			#   filesize = len(file['content'])<br />  
 			#   filetype = file['content-type']   
 
 			filename = file['filename']  
 
 			fd = open('%s/%s' % (MEDIA_ROOT, filename), 'wb')  
 			fd.write(file['content'])  
 			fd.close()  
 
 			return http.HttpResponseRedirect('upload_success.html')  
 	else:  
 		form = SimpleFileForm()  
 		return render_to_response(template, { 'form': form })  
 ```
###Template
fileupload.html
```python
 <head><title>upload test</title></head>
 {% block body  %}  
      <h1>Upload a file</h1>  
      <form action="." method="post" enctype="multipart/form-data">  
              {{ form }}  
              <input type="submit" value="Upload" />  
      </form>  
 {% endblock %}
 </html>
 ```



