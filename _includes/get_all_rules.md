{{ include.filename.description }}
{% for sect in include.filename.content %}
## {{ sect.section }}
    {% for stylerule in sect.sectionrules %}
{{ stylerule.rule | liquify }}
        {% for ex in stylerule.examples %}
* {{ ex | liquify }}
        {% endfor %}
    {% endfor %}
{% endfor %}