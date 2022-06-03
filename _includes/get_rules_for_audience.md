{{ include.filename.description }}
{% for sect in include.filename.rules %}
    {% for stylerule in sect.topics %}
        {% if stylerule.audience contains include.audience %}
## {{ sect.section }}
{% break %}
        {% endif %}
    {% endfor %}
    {% for stylerule in sect.topics %}
        {% if stylerule.audience contains include.audience %}
{{ stylerule.rule | liquify }}
            {% for ex in stylerule.examples %}
* {{ ex | liquify }}
            {% endfor %}
        {% endif %}
    {% endfor %}
{% endfor %}