# CS1102_Project
<!DOCTYPE html>
<html>
  <head>
  <title>CS1102 The Mechanism and Applications of Blockchain</title>
  <script> 
    var comment= []
    function addcomment(){
      var s,i;
    comment[comment.length]=document.getElementById("textinput").value;
      s="<ul>"
      for(i=0;i<comment.length;i++){
        s+="<li>"+comment[i]+"</li>";
        }
        s+="</ul>";
      document.getElementById("result").innerHTML=s;
      }
  </script>
  </head>
</html>
Yeung Ho Fung 57847209
Law Ho Tat 57317481
Ma Chun Chiu 57134824 
Chiu Tsz Ki 56615622
