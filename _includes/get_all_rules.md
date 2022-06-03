{{ include.filename.description }}
{% for sect in include.filename.rules %}
## {{ sect.section }}
    {% for stylerule in sect.topics %}
{{ stylerule.rule | liquify }}
        {% for ex in stylerule.examples %}
* {{ ex | liquify }}
        {% endfor %}
    {% endfor %}
{% endfor %}