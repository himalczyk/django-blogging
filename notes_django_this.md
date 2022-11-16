# Resource

https://realpython.com/python-django-blog/#demo-a-django-blog-admin-a-graphql-api-and-a-vue-front-end

# Configure django admin filtering,displaying etc

Create and register the PostAdmin class:

Allow filtering the post list by posts that are published or unpublished.
Allow filtering posts by publish date.
Allow editing all the displayed fields, with the exception of the ID.
Allow searching for posts using the title, subtitle, slug, and body.
Prepopulate the slug field using the title and subtitle fields.
Use the publish date of all posts to create a browsable date hierarchy.
Show a button at the top of the list to save changes.

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    model = Post

    list_display = (
        "id",
        "title",
        "subtitle",
        "slug",
        "publish_date",
        "published",
    )
    list_filter = (
        "published",
        "publish_date",
    )
    list_editable = (
        "title",
        "subtitle",
        "slug",
        "publish_date",
        "published",
    )
    search_fields = (
        "title",
        "subtitle",
        "slug",
        "body",
    )
    prepopulated_fields = {
        "slug": (
            "title",
            "subtitle",
        )
    }
    date_hierarchy = "publish_date"
    save_on_top = True

# Configuring Graphene-Django

Configure Graphene-Django
To get Graphene-Django working in your project, you’ll need to configure a few pieces:

Update settings.py so the project knows where to look for GraphQL information.
Add a URL pattern to serve the GraphQL API and GraphiQL, GraphQL’s explorable interface.
Create the GraphQL schema so Graphene-Django knows how to translate your models into GraphQL.

# CORS

The django-cors-headers project makes dealing with CORS fairly painless. You’ll use this to tell Django to respond to requests even if they come from another origin, which will allow the front end to communicate properly with the GraphQL API.