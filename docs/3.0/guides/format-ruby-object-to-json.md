# Pretty JSON objects to the code field

It's common to have JSON objects stored in your database. So you might want to display them nicely on your resource page.

```ruby
field :meta, as: :code, language: 'javascript'
```

<Image src="/assets/img/3_0/guides/format-ruby-object-to-json/before.png" width="806" height="584" alt="Avo Admin for Rails" />

But that will be hard to read on one line like that. So we need to format it.

Luckily we can use `JSON.pretty_generate` for that and a computed field.

```ruby{3}
field :meta, as: :code, language: 'javascript' do
  if record.meta.present?
    JSON.pretty_generate(record.meta.as_json)
  end
end
```

<Image src="/assets/img/3_0/guides/format-ruby-object-to-json/after.png" width="806" height="616" alt="Avo Admin for Rails" />

That's better! You'll notice that the field is missing on the `Edit` view. That's normal for a computed field to be hidden on `Edit`.
To fix that, we should add another one just for editing.

```ruby{1}
field :meta, as: :code, language: 'javascript', only_on: :edit
field :meta, as: :code, language: 'javascript' do
  if record.meta.present?
    JSON.pretty_generate(record.meta.as_json)
  end
end
```

Now you have a beautifully formatted JSON object in a code editor.
