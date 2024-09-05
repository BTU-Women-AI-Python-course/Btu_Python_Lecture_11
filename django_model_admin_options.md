Here are examples for each of the `ModelAdmin` options:

1. **`list_display`**  
   Defines which fields to display in the list view.
   ```python
   class BookAdmin(admin.ModelAdmin):
       list_display = ('title', 'author', 'published_date')
   ```

2. **`list_filter`**  
   Adds filters in the right sidebar of the list view.
   ```python
   class BookAdmin(admin.ModelAdmin):
       list_filter = ('author', 'published_date')
   ```

3. **`search_fields`**  
   Enables a search bar to search through the specified fields.
   ```python
   class BookAdmin(admin.ModelAdmin):
       search_fields = ('title', 'author__name')
   ```

4. **`list_editable`**  
   Makes fields editable directly from the list view.
   ```python
   class BookAdmin(admin.ModelAdmin):
       list_display = ('title', 'author', 'published_date', 'price')
       list_editable = ('price',)
   ```

5. **`list_per_page`**  
   Sets how many records to display per page.
   ```python
   class BookAdmin(admin.ModelAdmin):
       list_per_page = 20
   ```

6. **`list_select_related`**  
   Optimizes database queries by using `select_related` for related fields.
   ```python
   class BookAdmin(admin.ModelAdmin):
       list_select_related = ('author',)
   ```

7. **`readonly_fields`**  
   Makes certain fields read-only in the detail view.
   ```python
   class BookAdmin(admin.ModelAdmin):
       readonly_fields = ('isbn', 'created_at')
   ```

8. **`fieldsets`**  
   Groups fields into sections in the detail view.
   ```python
   class BookAdmin(admin.ModelAdmin):
       fieldsets = (
           ('Main Info', {
               'fields': ('title', 'author')
           }),
           ('Additional Info', {
               'fields': ('published_date', 'price')
           }),
       )
   ```

9. **`filter_horizontal`**  
   Displays a ManyToMany field with a horizontal filter widget.
   ```python
   class BookAdmin(admin.ModelAdmin):
       filter_horizontal = ('genres',)
   ```

10. **`filter_vertical`**  
    Displays a ManyToMany field with a vertical filter widget.
    ```python
    class BookAdmin(admin.ModelAdmin):
        filter_vertical = ('tags',)
    ```

11. **`inlines`**  
    Adds inline related objects in the detail view.
    ```python
    class ChapterInline(admin.TabularInline):
        model = Chapter

    class BookAdmin(admin.ModelAdmin):
        inlines = [ChapterInline]
    ```

12. **`prepopulated_fields`**  
    Automatically populates a field based on the value of another field.
    ```python
    class BookAdmin(admin.ModelAdmin):
        prepopulated_fields = {'slug': ('title',)}
    ```

13. **`save_on_top`**  
    Moves the save buttons to the top of the form in addition to the bottom.
    ```python
    class BookAdmin(admin.ModelAdmin):
        save_on_top = True
    ```

14. **`exclude`**  
    Excludes certain fields from the form.
    ```python
    class BookAdmin(admin.ModelAdmin):
        exclude = ('isbn',)
    ```

These examples showcase how to use each option in `ModelAdmin` to customize Django's admin interface.
