{%- comment -%}
  Tag-only lines use left-trim markers so they leave no output of their own. Left-trim also removes
  blank lines before a tag, so put Markdown blank lines after a tag instead.
{%- endcomment -%}
{%- assign resume = site.data.resume -%}
{%- assign basics = resume.basics -%}
# {{ basics.name }} - Resume
[website]({{ basics.url }}){% for profile in basics.profiles %} | [{{ profile.network | downcase }}]({{ profile.url }}){% endfor %}

{{ basics.summary }}

## Skills
{% for skill in resume.skills %}
  {%- if skill.name == "Core strengths" %}
    {%- for keyword in skill.keywords %}
* {{ keyword }}
    {%- endfor %}
  {%- endif %}
{%- endfor %}

## Technical Skills
{% for skill in resume.skills %}
  {%- unless skill.name == "Core strengths" %}
* **{{ skill.name }}:** {{ skill.keywords | join: ", " }}
  {%- endunless %}
{%- endfor %}

## Experience
{%- assign companies = resume.work | group_by: "name" %}
{%- for company in companies %}
  {%- assign first_role = company.items | first %}

### {{ company.name }}

[Website]({{ first_role.url }})

**Technologies:**  
{{ first_role.keywords | join: ", " }}
  {%- for role in company.items %}
    {%- assign started = role.startDate | append: "-01" | date: "%B %Y" %}
    {%- assign ended = "Present" %}
    {%- if role.endDate %}
      {%- assign ended = role.endDate | append: "-01" | date: "%B %Y" %}
    {%- endif %}

#### {{ role.position }}

_{{ started }} - {{ ended }}_
    {%- if role.summary %}

{{ role.summary }}
    {%- endif %}
    {%- if role.highlights %}
{% for highlight in role.highlights %}
- {{ highlight }}
      {%- endfor %}
    {%- endif %}
  {%- endfor %}
{%- endfor %}

## Education
{%- for school in resume.education %}

### {{ school.institution }}
**Graduating Year:** {{ school.endDate }}  
{{ school.studyType }}. Elective courses: {{ school.courses | join: ", " }}.
{%- endfor %}
