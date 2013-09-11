# QiniuDirectUploader

This Gem can direct upload you files to a Qiniu storage bucket

## Installation

Add this line to your application's Gemfile:

    gem 'qiniu_direct_uploader'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install qiniu_direct_uploader

## Usage

see the example project: https://github.com/huobazi/qiniu-direct-upload-example

### Views
```erb
<%= qiniu_uploader_form callback_url: items_path,
      bucket:        'spec-test',
      id:            "photograph-uploader",
      key:           "{timestamp}-{unique-id}-#{SecureRandom.hex}-{filename}",
      custom_fields: {aaa:1,bbb:2},
      progress_bar_id: 'progress-bar',
      drop_paste_zone_id: 'dropzone',
      store_path:    "/items/#{Date.today.strftime('%Y/%m')}" do %>

      <div class="bars" id="progress-bar">
        <%= file_field_tag :file, multiple: true, accept: "image/gif, image/jpeg" %> You can also drag and drop files here
      </div>
<% end %>
```
### Javascript
```coffee
$(document).ready ->
  photoForm = $("form#photograph-uploader")
  if photoForm.length > 0
    photoForm.QiniuUploader
      customCallbackData: {"xyz": 100}
      onFilesAdd: (file) ->
        if file.type != "image/jpeg"
          alert('please select image')
          return false
        else
          return true

    photoForm.bind "ajax:success", (e, data) ->
      console.log('success')
      console.log(data)

    photoForm.bind "ajax:failure", (e, data) ->
      console.log('failure')
      console.log(data)
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
