# Changing hardcoded limits

Make sure to recompile assets after making these edits for your changes to take effect. 

## Toots

### How to change character limits in toots

1. Edit `app/validators/status_length_validator.rb`
2. On line #4, change `MAX_CHARS` from 500 to your desired maximum.
3. Edit `app/javascript/mastodon/features/compose/components/compose_form.js`
4. On line #202, change `CharacterCounter max={500}` to the same max value as before
5. On line #206, change `length(text) > 500` to the same max value as before

## Accounts

### How to change character limits in bios

1. Edit `app/models/account.rb`
2. On line #78, change `validates :note, note_length: { maximum: 500 }` to your desired maximum

1. Edit `app/views/settings/profiles/show.html.haml`
2. On line #10, change `input_html: { maxlength: 500 }` to your desired maximum

### How to add more profile fields

1. Edit `app/models/account.rb`
2. On line #79, change `validates :fields, length: { maximum: 4 }` to your desired maximum
3. On line #262, change `DEFAULT_FIELDS_SIZE = 4` to the same max value as before

### How to change character limits in profile fields

1. Edit `app/models/account.rb`
2. On lines #366-370, define your own `string_limit`. You will probably be most interested in changing `if account.local? 255` to something <= 2047, since vanilla instances will refuse your fields as invalid if they are longer than this. You can also optionally decide to accept remote profile fields that are longer than 2047 characters (but why would you, if virtually all are below this?), or be more strict and only accept shorter profile fields.
