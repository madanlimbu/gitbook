# CRLF will be replaced by LF

#### Problem Summary

We have probably come across this warning in git. This usually caused by git repo file being used in different system \( DOS/Unix \).

Text files created on DOS/Window has different line ending comparing to Unix/Linux. DOS has both `carriage return` and `line feed` `\r\n` as a line ending, whereas Unix use just `line feed` `\n` . 

This difference in line ending will throw git warning `CRLF will be replaced by LF` when we clone a project created on DOS/Window to Unix as git auto-convert the files to Unix line endings.

#### Solution

We can add config on git to convert all CRLF line endings to LF before it is stored in commit.

```text
git config --global core.autocrlf input
```

We can then make sure git doesn't add changes for line-ending by adding following config:

```text
git config --global core.safecrlf true
```

Finally, we can set line ending properties on a repo by using `.gitattributes` file which will be committed to the repo and overrides the`core.autocrlf` setting.

{% code title=".gitattributes" %}
```text
* text eol=lf
```
{% endcode %}

#### Note: we can run following command to convert CRLF to LF and update .gitattributes file to auto enforce LF line endings.

```text
find ./ -type f -exec dos2unix {} \;
```

