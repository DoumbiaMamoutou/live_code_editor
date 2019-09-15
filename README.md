# live_code_editor

#MODELES LIVE CODE EDITOR

## MES TABLES
* UserQuest
* Module
* Semaine
* Test
* Quest
* ExerciceTest
* ExerciceQuest

### MODELE Module
```
#...
class Module(models.Model):
  module_id = models.PositiveIntegerField(default=1, null=True, blank=True)
  nom_module = models.CharField(max_length=255)
  image_module = models.ImageField(upload_to='module')
  status = models.BooleanField(default=False)
  usages = models.TextField()
  debut = models.DateField(null=True)
  mode = models.CharField(max_length=255, null=True)
  date_add = models.DateTimeField(auto_now_add=True)
  date_up = models.DateTimeField(auto_now=True)
#...
```

### MODELE Semaine
```
#...
class Semaine(models.Model):
  module_id = models.ForeignKey(Module, on_delete=models.CASCADE, null=True, related_name='module_semaine')
  titre = models.CharField(max_length=255)
  description = models.TextField()
  debut_sem = models.DateTimeField(auto_now=False, null=True)
  fin_sem = models.DateTimeField(auto_now=False, null=True)
  date_add = models.DateTimeField(auto_now_add=True)
  date_up = models.DateTimeField(auto_now=True)
  status = models.BooleanField(default=False)
  
#...
```

### MODELE Test
```
#...
class Test(models.Model):
  semaine_test_id = models.ForeignKey(Semaine, on_delete=models.CASCADE, null=True, related_name='semaine_test')
  nom_test = models.CharField(max_length=255)
  description_test = models.TextField()
  status = models.BooleanField(default=False)
  last_sem = models.BooleanField(default=False)
  dure_test = models.IntegerField()
  autorise_test = models.BooleanField(default=False)
  date_add = models.DateTimeField(auto_now_add=True)
  date_up = models.DateTimeField(auto_now=True)
  
#...
```

### MODELE Quest
```
#...
class Quest(models.Model):
  sem_quest = models.ForeignKey(Semaine, on_delete=models.CASCADE, null=True, related_name='sem_quest')
  name = models.CharField(max_length=255)
  description = models.TextField()
  status = models.BooleanField()
  debut_quest = models.DateTimeField(auto_now=False)
  fin_quest = models.DateTimeField(auto_now_add=False)
  date_add = models.DateTimeField(auto_now_add=True)
  date_up = models.DateTimeField(auto_now=True)
  
#...
```
### MODELE ExerciceTest
```
#...
class ExerciceTest(models.Model):
  semaine_test_exo_id = models.ForeignKey(Test, on_delete=models.CASCADE, null=True, related_name='test_exo')
  nom = models.CharField(max_length=255)
  description = models.TextField()
  guide = models.TextField()
  statut = models.BooleanField(default=False)
  code_source = models.TextField(null=True)
  code_solution = models.TextField(null=True)
  duree = models.IntegerField(null=True, default=1, blanl=True)
  date_ad = models.DateTimeField(auto_now_add=True)
  date_up = models.DateTimeField(auto_now=True)
#...
```

### MODELE ExerciceQuest
```
#...
class ExerciceQest(models.Model):
  semaine_quest_exo_id = models.ForeignKey(Quest, on_delete=models.CASCADE, null=True, related_name='quest_exo')
  nom = models.CharField(max_length=255)
  description = models.TextField()
  statut = models.BooleanField(default=False)
  code_source = models.TextField(null=True)
  code_solution = models.TextField(null=True)
  duree = models.IntegerField(null=True, default=1, blanl=True)
  date_ad = models.DateTimeField(auto_now_add=True)
  date_up = models.DateTimeField(auto_now=True)
#...
```

```#______________________ LIAISON AVEC USER DE DJANGO _________________#```
### MODELE UserQuest
```
#...
class UserQuest(models.Model):
  user_quest = models.ManyToMany(User)
  nom = models.CharField(max_length=255)
  quest_id_user = models.ForeignKey(Quest, on_delete=models.CASCADE, null=True, related_name='userquest')
  date_ad = models.DateTimeField(auto_now_add=True)
  date_up = models.DateTimeField(auto_now=True)
#...
```
