# Grid view

<br>
<Image src="/assets/img/grid-view.jpg" width="1312" height="1096" alt="Avo grid view" />

Some resources are best displayed in a grid view. We can do that with Avo using a `cover_url`, a `title`, and a `body`.

## Enable grid view

To enable grid view for a resource, you need to configure the `grid_view` class attribute on the resource. That will add the grid view to the view switcher on the <Index /> view.

```ruby{2-13}
class Avo::Resources::Post < Avo::BaseResource
  self.grid_view = {
    card: -> do
      {
        cover_url:
          if record.cover_photo.attached?
            main_app.url_for(record.cover_photo.url)
          end,
        title: record.name,
        body: record.truncated_body
      }
    end
  }
end
```

<Image src="/assets/img/view-switcher.png" width="822" height="153" alt="Avo view switcher" />

## Make default view

To make the grid the default way of viewing a resource **Index**, we have to use the `default_view_type` class attribute.

```ruby{2}
class Avo::Resources::Post < Avo::BaseResource
  self.default_view_type = :grid
end
```

## Custom style

You may want to customize the card a little bit. That's possible using the `html` option.

```ruby{13-37}
class Avo::Resources::Post < Avo::BaseResource
  self.grid_view = {
    card: -> do
      {
        cover_url:
          if record.cover_photo.attached?
            main_app.url_for(record.cover_photo.url)
          end,
        title: record.name,
        body: record.truncated_body
      }
    end,
    html: -> do
      {
        title: {
          index: {
            wrapper: {
              classes: "bg-blue-50 rounded-md p-2"
            }
          }
        },
        body: {
          index: {
            wrapper: {
              classes: "bg-gray-50 rounded-md p-1"
            }
          }
        },
        cover: {
          index: {
            wrapper: {
              classes: "blur-sm"
            }
          }
        }
      }
    end
  }
end
```

<Image src="/assets/img/grid-html-option.png" width="1014" height="637" alt="Grid html option" />

