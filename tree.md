class Enrollment(TimeStampedModelWithUser):
    student = models.ForeignKey(
        "Student", 
        on_delete=models.CASCADE, 
        related_name="enrollments",
        verbose_name=_("Élève")
    )
    classroom = models.ForeignKey(
        "Classroom", 
        on_delete=models.PROTECT, 
        related_name="enrollments",
        verbose_name=_("Classe")
    )
    school_year = models.ForeignKey(   # Changed from schoolyear to school_year
        "SchoolYear", 
        on_delete=models.PROTECT, 
        related_name="enrollments",
        verbose_name=_("Année scolaire")
    )
    enrollment_date = models.DateField(
        auto_now_add=True,
        verbose_name=_("Date d'inscription")
    )
    is_active = models.BooleanField(
        default=True,
        verbose_name=_("Inscription active")
    )

    class Meta:
        # ... constraints and indexes ...

    def clean(self):
        # ... validation using self.school_year ...

    def __str__(self):
        return f"{self.student.full_name} - {self.classroom.full_name} ({self.school_year.name})"