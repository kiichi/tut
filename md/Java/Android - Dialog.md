
##Android - Dialog

###Input
```java
 final EditText textEdit = new EditText(this);
 
 // Builder
 AlertDialog.Builder alert = new AlertDialog.Builder(this);
 alert.setTitle("Enter text");
 alert.setView(textEdit);
 
 alert.setPositiveButton("Ok", new DialogInterface.OnClickListener() {
     @Override
     public void onClick(DialogInterface dialog, int which) {
         String text = textEdit.getText().toString();
         finish();
     }
 });
 
 alert.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
     @Override
     public void onClick(DialogInterface dialog, int which) {
         finish();
     }
 });
 
 // Dialog
 AlertDialog dialog = alert.create();
 dialog.setOnShowListener(new OnShowListener() {
 
     @Override
     public void onShow(DialogInterface dialog) {
         InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
         imm.showSoftInput(textEdit, InputMethodManager.SHOW_IMPLICIT);
     }
 });
 
 dialog.show();
 ```


