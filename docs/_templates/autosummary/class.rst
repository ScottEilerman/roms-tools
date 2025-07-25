{{ objname | escape | underline}}

.. currentmodule:: {{ module }}

.. autoclass:: {{ objname }}
   :members:
   :exclude-members: model_config
   :inherited-members: BaseModel, pydantic.BaseModel, pydantic.main.BaseModel
   {% block methods %}
   {% if methods %}
   .. rubric:: Methods
   .. autosummary::
      :toctree:
   {% for item in methods %}
      {%- if not item.startswith('_') or item in ['__call__',
                                                  ] %}
        {%- if not (objname == 'ChildGrid' and item == 'from_file') %}
        {%- if not item in inherited_members %}
            {{ name }}.{{ item }}
        {% endif %}
      {% endif %}
    {% endif %}
   {% endfor %}
   {% endif %}
   {% endblock %}

   {% block attributes %}
   {% if attributes %}
   .. rubric:: Attributes
   .. autosummary::
   {% for item in attributes %}
    {%- if not item in inherited_members %}
      {{ name }}.{{ item }}
    {% endif %}
   {% endfor %}
   {% endif %}
   {% endblock %}
