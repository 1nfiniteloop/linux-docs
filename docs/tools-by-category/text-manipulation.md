# Text manipulation

## Tools

* `column` - Format text into columns.
* `envsubst` - substitutes (exported) environment variables from stdin.
* `fold` - Wrap input lines in file
* `cut` - Print selected parts of lines.
* `sed` - Text stream editor.
* `sort` - sort lines of text .
* `uniq` - report or omit repeated lines.
* `wc` - Words and lines count.

## Usage

### sed

Common used flags:

* `-i|--in-place[=<BACKUP-SUFFIX>]`
* `-r|--regexp-extended`

Command                                          | Description
-------------------------------------------------|---------------------------------------------
`sed 's/original-text/substitute-text/g' <file>` | Substituting text
`sed '/^this-text/d; /^or-this/d' <file>`        | Substituting text, multiple matches
`sed '/original-text/d' <file>`                  | Remove line(s) containing text
`sed -i -r 's|\s*$||g' <FILE>`                   | remove trailing whitespaces (in source code)
`sed -i -r 's|\t|    |g' <FILE>`                 | Replace tab indentions with spaces

### fold

* Break lines in a text file after 80 characters on whitespace: `fold --spaces <file>`

### column

* Present result in a proper aligned table: `grep -r 'some-text'  build/ |column -t`

### cut

* Example: Get user's full name:

        getent passwd ${USER} \
          |cut --delimiter=':' --field=4 \
          |cut --delimiter=',' --field=5
