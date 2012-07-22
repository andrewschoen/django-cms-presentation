.. django CMS: Friends don't let friends use Drupal master file, created by Andrew Schoen


django CMS: Friends don't let friends use Drupal
================================================

Andrew Schoen | @andrewschoen | @pythonkc

.. include:: _templates/pykc-logo.rst

 
CMS? Content Management System?
===============================

A **collection of content** *(words, pictures, files, events, news articles, schedules, employee bios, blog posts, videos, etc.)* **organized into menus.**

.. include:: _templates/pykc-logo.rst

Too Many Options
----------------

* Drupal
* Expression Engine
* Wordpress
* Umbraco
* Sitecore
* Ektron
* Joomla
* Teamsite

.. include:: _templates/pykc-logo.rst

We all love Python & Django, can we have a CMS and use those too?
=================================================================

.. include:: _templates/pykc-logo.rst

Yes! django CMS!
================

https://www.django-cms.org/

https://github.com/divio/django-cms

http://docs.django-cms.org/

@djangocms @divio

#django-cms

.. include:: _templates/pykc-logo.rst


Why django CMS?
===============

All the CMS features you want without the added complexity of most
other options out there.

**Python!**

**Django!**

**Awesome!**

.. include:: _templates/pykc-logo.rst

All the Features!
-----------------

* Page & Menu Creation
* User Management
* User Permissions
* Page Moderation
* Multi-site
* Multi-lingual
* Frontend Editing
* Plugin system

Plus, everything that comes with Django. That's a lot.

.. image:: images/all_the_features.jpeg
   :class: all-the-features

.. include:: _templates/pykc-logo.rst

Templates
=========

Templates are the building blocks of content in a CMS.  

Pages are created by templates and attached to menus.

In django CMS, templates have placeholders and placeholders have plugins.

.. include:: _templates/pykc-logo.rst

Templates
---------

base.html

::

    {% load cms_tags sekizai_tags %}
    <html>
      <head>
          {% render_block 'css' %}
      </head>
      <body>
          {% cms_toolbar %}
          <ul>{% show_menu %}</ul>
          {% block base_content %}{% endblock %}
          {% render_block 'js' %}
      </body>
    </html>

.. include:: _templates/pykc-logo.rst

Templates
---------

home.html

::

    {% extends "base.html" %}
    {% load cms_tags %}

    {% block base_content %}
      {% placeholder homepage_content %}
    {% endblock %}

.. include:: _templates/pykc-logo.rst


Template Tags & Settings
========================

Commonly used template tags and settings for creating templates.

.. include:: _templates/pykc-logo.rst

CMS_TEMPLATES
-------------

::

    CMS_TEMPLATES = (
        ('home.html', gettext('Homepage')),
        ('2col.html', gettext('2 Column')),
        ('3col.html', gettext('3 Column')),
        ('extra.html', gettext('Some extra fancy template')),
    )

.. include:: _templates/pykc-logo.rst

placeholder
-----------

::

    {% placeholder "homepage_content" %}

    {% placeholder "homepage_content" or %}
        <p>Default content goes here</p>
    {% endplaceholder %}

    {% with 320 as width %}{% placeholder "home_content" %}{% endwith %}

    {% placeholder "home_content" inherit %}

.. include:: _templates/pykc-logo.rst

CMS_PLACEHOLDER_CONF
++++++++++++++++++++

::

    CMS_PLACEHOLDER_CONF = {
        'home_content': {
            'plugins': ['TextPlugin', 'PicturePlugin'],
            'text_only_plugins': ['LinkPlugin']
            'extra_context': {"width":640},
            'name':gettext("Content"),
        },
        'right-column': {
            "plugins": ['TeaserPlugin', 'LinkPlugin'],
            "extra_context": {"width":280},
            'name':gettext("Right Column"),
            'limits': {
                'global': 2,
                'TeaserPlugin': 1,
                'LinkPlugin': 1,
            },
        },
    }

.. include:: _templates/pykc-logo.rst

show_placeholder
----------------

::

    {% show_placeholder "footer" "footer_container_page" %}
    {% show_placeholder "content" request.current_page.parent_id %}
    {% show_placeholder "teaser" request.current_page.get_root %}

    {% placeholder "teaser" or %}
        {% show_placeholder "teaser" request.current_page.get_root %}
    {% endplaceholder %}

.. include:: _templates/pykc-logo.rst

page tags
---------

page_url & page_attribute

::

    <a href="{% page_url "help" %}">Help page</a>
    <a href="{% page_url request.current_page.parent %}">Parent page</a>

    # options for page_attribute:
    # "title", "menu_title", "page_title", 
    # "slug", "meta_description", "meta_keywords"

    {% page_attribute "page_title" %}
    {% page_attribute "meta_description" "my_page_reverse_id" %}
    {% page_attribute "meta_keywords" request.current_page.parent_id %}
    {% page_attribute "slug" request.current_page.get_root %}

.. include:: _templates/pykc-logo.rst

menu tags
---------

**show_menu & show_menu_below_id**

::

    # start_level, end_level, extra_inactive, extra_active

    {% show_menu 0 100 0 100 %} # default
    {% show_menu 0 100 100 100 "myapp/menu.html" %}

    {% show_menu_below_id "meta" %}
    {% show_menu_below_id "meta" 0 100 100 100 "myapp/menu.html" %}

**show_sub_menu & show_breadcrumb**

::

    {% show_sub_menu 1 %}  
    {% show_breadcrumb 2 "myapp/breadcrumb.html" %}


.. include:: _templates/pykc-logo.rst

settings
--------

::

    CMS_URL_OVERWRITE = True
    CMS_MENU_TITLE_OVERWRITE = False
    CMS_REDIRECTS = False
    CMS_SOFTROOT = False
    CMS_PERMISSION = False
    CMS_PUBLIC_FOR = all # or staff
    CMS_MODERATOR = False
    CMS_SHOW_START_DATE = False
    CMS_SHOW_END_DATE = False
    CMS_SEO_FIELDS = False
    CMS_CACHE_DURATIONS = {
        "content": 3600,
        "menus": 3600,
        "permissions": 3600,
    }
    CMS_CACHE_PREFIX = "cms-"

.. include:: _templates/pykc-logo.rst

settings
--------

::

    CMS_HIDE_UNTRANSLATED = True
    CMS_LANGUAGES = (
        ('de', gettext('German')),
        ('en', gettext('English')),
    )
    CMS_LANGUAGE_FALLBACK = True
    CMS_LANGUAGE_CONF = {
        'de': ['en', 'fr'],
        'en': ['de'],
    }
    CMS_SITE_LANGUAGES = {
        1:['en','de'],
        2:['en','fr'],
    }
    CMS_FRONTEND_LANGUAGES = ("de", "en", "fr")

.. include:: _templates/pykc-logo.rst


Plugins
=======

Apphooks
========

Menus
=====

Demo
====

Closing
=======



        






    


    









