# live_code_editor

#MODELES LIVE CODE EDITOR

## MES TABLES
* User de django
* Module
* Semaine
* Test
* Quest

### MODELE Module
#...
class Module(models.Model):
  nom_module = models.CharField(max_length=100)
  status = models.BooleanField(default=False)
  user = models.ForignKey(User, on_delete=models.CASCADE, related_name='user_module')
#...
  
### MODELE Semaine
class Semaine(models.Model):
  numero_semaine = models.PositiveIntegerField()
  status = models.BooleanField(default=False)
  semaine_mod = models.ManyToMany('Module')
  
### MODELE Test
class Test(models.Model):
  nom_test = models.CharField(max_length=50)
  status = models.BooleanField(default=False)
  titre_test = models.CharField(max_length=100)
  dure_test = models.DurationField()
  test = models.ForeignKey('Semaine', on_delete=models.CASCADE, related_name='semaine_test')
  
### MODELE Quest
class Quest(models.Model):
  description = models.TextField()
  status = models.BooleanField()
  quest_test = models.ForeignKey('Test', on_delete=models.CASCADE, related_name='test_quest')
  

'''
