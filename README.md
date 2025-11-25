
# 📌 **models.py — Centro de Idiomas (Markdown para README.md)**

````markdown
# 📚 Models — Sistema de Gestión de Centro de Idiomas

A continuación se presenta el archivo `models.py` utilizado para gestionar idiomas, cursos, estudiantes, profesores, materiales, inscripciones y evaluaciones dentro del sistema.

```python
from django.db import models


# ===========================
#       IDIOMA
# ===========================
class Idioma(models.Model):
    nombre_idioma = models.CharField(max_length=50)
    familia_linguistica = models.CharField(max_length=50)
    nivel_dificultad_promedio = models.CharField(max_length=20)
    num_hablantes_estimado = models.BigIntegerField()
    es_popular = models.BooleanField()

    def __str__(self):
        return self.nombre_idioma


# ===========================
#       CURSO_IDIOMA
# ===========================
class CursoIdioma(models.Model):
    nombre_curso = models.CharField(max_length=100)
    id_idioma = models.ForeignKey(Idioma, on_delete=models.CASCADE, related_name='cursos')
    nivel_curso = models.CharField(max_length=50)
    duracion_semanas = models.IntegerField()
    precio = models.DecimalField(max_digits=10, decimal_places=2)
    cupo_maximo = models.IntegerField()
    horario_clase = models.CharField(max_length=100)
    material_incluido = models.TextField()
    fecha_inicio_oferta = models.DateField()

    def __str__(self):
        return self.nombre_curso


# ===========================
#     ESTUDIANTE_IDIOMA
# ===========================
class EstudianteIdioma(models.Model):
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    fecha_nacimiento = models.DateField()
    email = models.CharField(max_length=100)
    telefono = models.CharField(max_length=20)
    idioma_nativo = models.CharField(max_length=50)
    fecha_inscripcion = models.DateField()
    nivel_conocimiento_idioma = models.CharField(max_length=50)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"


# ===========================
#     PROFESOR_IDIOMA
# ===========================
class ProfesorIdioma(models.Model):
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    email = models.CharField(max_length=100)
    telefono = models.CharField(max_length=20)
    idioma_enseñanza = models.CharField(max_length=50)
    nivel_dominio = models.CharField(max_length=50)
    fecha_contratacion = models.DateField()
    salario_hora = models.DecimalField(max_digits=5, decimal_places=2)
    nacionalidad = models.CharField(max_length=50)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"


# ===========================
#     INSCRIPCION_IDIOMA
# ===========================
class InscripcionIdioma(models.Model):
    id_estudiante = models.ForeignKey(EstudianteIdioma, on_delete=models.CASCADE, related_name='inscripciones')
    id_curso = models.ForeignKey(CursoIdioma, on_delete=models.CASCADE, related_name='inscripciones')
    fecha_inscripcion = models.DateField()
    estado_inscripcion = models.CharField(max_length=50)
    nota_final_curso = models.DecimalField(max_digits=4, decimal_places=2)
    fecha_finalizacion = models.DateField()
    id_profesor_asignado = models.ForeignKey(ProfesorIdioma, on_delete=models.CASCADE, related_name='inscripciones')

    def __str__(self):
        return f"Inscripción {self.id} - Estudiante {self.id_estudiante}"


# ===========================
#     MATERIAL_DIDACTICO
# ===========================
class MaterialDidactico(models.Model):
    nombre_material = models.CharField(max_length=255)
    tipo_material = models.CharField(max_length=50)
    descripcion = models.TextField()
    editorial = models.CharField(max_length=100)
    costo = models.DecimalField(max_digits=10, decimal_places=2)
    id_idioma = models.ForeignKey(Idioma, on_delete=models.CASCADE, related_name='materiales')
    nivel_asociado = models.CharField(max_length=50)
    fecha_publicacion = models.DateField()
    es_obligatorio = models.BooleanField()

    def __str__(self):
        return self.nombre_material


# ===========================
#     EVALUACION_IDIOMA
# ===========================
class EvaluacionIdioma(models.Model):
    id_inscripcion = models.ForeignKey(InscripcionIdioma, on_delete=models.CASCADE, related_name='evaluaciones')
    tipo_evaluacion = models.CharField(max_length=50)
    fecha_evaluacion = models.DateField()
    puntaje_obtenido = models.DecimalField(max_digits=5, decimal_places=2)
    ponderacion = models.DecimalField(max_digits=3, decimal_places=2)
    comentarios_profesor = models.TextField()
    habilidades_evaluadas = models.TextField()

    def __str__(self):
        return f"Evaluación {self.id} - Inscripción {self.id_inscripcion_id}"
````

```

---
