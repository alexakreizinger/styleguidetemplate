{% assign titleLoop = 0 %}
{% for sect in include.filename.rules %}
    {% for stylerule in sect.topics %}
        {% if stylerule.audience contains include.audience and stylerule.featured and titleLoop == 0 %}
### [{{ include.sectionname }}]({{ include.sectionlink }})
{% assign titleLoop = titleLoop | plus: 1 %}
{% break %}
        {% endif %}
    {% endfor %}
{% endfor %}

{% for sect in include.filename.rules %}
    {% for stylerule in sect.topics %}
        {% if stylerule.audience contains include.audience and stylerule.featured %}
* {{ stylerule.featured | liquify }}
        {% endif %}
    {% endfor %}
{% endfor %}