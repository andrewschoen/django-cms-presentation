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

cms_placeholder_conf
--------------------

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

language tags
-------------

page_language & language_chooser

::

    {% page_language_url de %}
    {% page_language_url fr %}
    {% page_language_url en %}

    {% language_chooser %}
    {% language_chooser "myapp/language_chooser.html" %}

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

Plugins are the content in django CMS.  You can use the built-in plugins, but
the real power of plugins come from building your own.

.. include:: _templates/pykc-logo.rst

built-in plugins
----------------

* 'cms.plugins.file'
* 'cms.plugins.flash'
* 'cms.plugins.googlemap'
* 'cms.plugins.link'
* 'cms.plugins.picture'
* 'cms.plugins.snippet'
* 'cms.plugins.teaser'
* 'cms.plugins.text'
* 'cms.plugins.video'
* 'cms.plugins.twitter'

.. include:: _templates/pykc-logo.rst

Writing your own Plugins
========================

The built-in plugins work for some situations, but it is really easy to write you own and add a ton of flexibility to the CMS.  With custom plugins you can integrate just about any other data (content) into CMS pages.

.. include:: _templates/pykc-logo.rst

custom plugins
--------------

We're going to be extending the standard Django Poll app from the tutorial.  First, we'll create our model. Make sure to ``syncdb``.

::

    from cms.models import CMSPlugin

    class PollPlugin(CMSPlugin):
        poll = models.ForeignKey('polls.Poll', related_name='plugins')

        def __unicode__(self):
          return self.poll.question

.. include:: _templates/pykc-logo.rst

custom plugins
--------------

Next, we need to create our plugin class.

::
    
    from cms.plugin_base import CMSPluginBase
    from cms.plugin_pool import plugin_pool
    from polls.models import PollPlugin as PollPluginModel
    from django.utils.translation import ugettext as _

    class PollPlugin(CMSPluginBase):
        model = PollPluginModel # Model where data about this plugin is saved
        name = _("Poll Plugin") # Name of the plugin
        render_template = "polls/plugin.html" # template to render the plugin with

        def render(self, context, instance, placeholder):
            context.update({'instance':instance})
            return context

    plugin_pool.register_plugin(PollPlugin) # register the plugin

.. include:: _templates/pykc-logo.rst

custom plugins
--------------

Finally, we need to create the template our plugin will render.

::

    <h1>{{ instance.poll.question }}</h1>

    <form action="{% url polls.views.vote instance.poll.id %}" method="post">
    {% csrf_token %}
    {% for choice in instance.poll.choice_set.all %}
        <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}" />
        <label for="choice{{ forloop.counter }}">{{ choice.choice }}</label><br />
    {% endfor %}
    <input type="submit" value="Vote" />
    </form>

.. include:: _templates/pykc-logo.rst

custom plugins
--------------

That's it!  Your poll app should now look like this.

::

    polls/
        templates/
            polls/
                plugin.html
        __init__.py
        cms_plugins.py
        models.py
        tests.py
        views.py

.. include:: _templates/pykc-logo.rst

Apphooks
========

Sometimes a plugin just isn't enough.  You can hook your own django apps into a CMS page using apphooks.

CMS apps live in a file called cms_apps.py within your app folder.

.. include:: _templates/pykc-logo.rst

apphooks
--------

Create cms_apps.py in the polls app and write this.

::

    from cms.app_base import CMSApp
    from cms.apphook_pool import apphook_pool
    from django.utils.translation import ugettext_lazy as _

    class PollsApp(CMSApp):
        name = _("Poll App") # give your app a name, this is required
        urls = ["polls.urls"] # link your app to url configuration(s)

    apphook_pool.register(PollsApp) # register your app

**Make sure to remove your app from urls.py**

.. include:: _templates/pykc-logo.rst

apphooks
--------

Now open your admin in your browser and edit a CMS Page. Open the ‘Advanced Settings’ tab and choose ‘Polls App’ for your ‘Application’.

Unfortunately, for these changes to take effect, you will have to restart your server. So do that and afterwards if you navigate to that CMS Page, you will see your polls application.

.. include:: _templates/pykc-logo.rst

apphooks
--------

Really, that's it.  Now whenever a user clicks on that page they will be taken to your own custom app.

Your polls app should now look like this.

::
    
    polls/
        templates/
            polls/
                plugin.html
        __init__.py
        cms_apps.py
        cms_plugins.py
        models.py
        tests.py
        views.py


.. include:: _templates/pykc-logo.rst

Custom Menus
============

Your apphook might have some custom navigation you want to include in the menu.  This is how you accomplish that.

First, create a menus.py in the polls app.


.. include:: _templates/pykc-logo.rst

custom menus
------------

::

    from cms.menu_bases import CMSAttachMenu
    from menus.base import Menu, NavigationNode
    from menus.menu_pool import menu_pool
    from django.core.urlresolvers import reverse
    from django.utils.translation import ugettext_lazy as _
    from polls.models import Poll

    class PollsMenu(CMSAttachMenu):
        name = _("Polls Menu") # give the menu a name, this is required.

        def get_nodes(self, request):
            nodes = []
            for poll in Poll.objects.all():
                node = NavigationNode(
                    poll.question,
                    reverse('polls.views.detail', args=(poll.pk,)),
                    poll.pk
                )
                nodes.append(node)
            return nodes
    menu_pool.register_menu(PollsMenu) # register the menu.

.. include:: _templates/pykc-logo.rst

custom menus
------------

Now, we need to attach this menu to the apphook.

polls/cms_apps.py

::

    from cms.app_base import CMSApp
    from cms.apphook_pool import apphook_pool
    from polls.menus import PollsMenu
    from django.utils.translation import ugettext_lazy as _

    class PollsApp(CMSApp):
        name = _("Poll App")
        urls = ["polls.urls"]
        menus = [PollsMenu] # attach a CMSAttachMenu to this apphook.
    apphook_pool.register(PollsApp)

.. include:: _templates/pykc-logo.rst

custom menus
------------

Doesn't get any easier.  Your polls app should look like this now.

::

    polls/
        templates/
            polls/
                plugin.html
        __init__.py
        cms_apps.py
        cms_plugins.py
        menus.py
        models.py
        tests.py
        views.py

.. include:: _templates/pykc-logo.rst

Extensions
==========

Some 3rd party apps you might want to try out.

.. include:: _templates/pykc-logo.rst

extensions
----------

django-filer: https://github.com/stefanfoulis/django-filer

cmsplugin-filer: https://github.com/stefanfoulis/cmsplugin-filer

django-reversion: https://github.com/etianen/django-reversion

cmsplugin-blog: https://github.com/fivethreeo/cmsplugin-blog

.. include:: _templates/pykc-logo.rst

Demo Time!
==========

.. include:: _templates/pykc-logo.rst

Just kidding, but I built you one. Download the code and run it locally, it's easy.
===================================================================================

https://github.com/andrewschoen/django-cms-demo

.. include:: _templates/pykc-logo.rst

Thanks!
=======

Andrew Schoen | @andrewschoen | @pythonkc

https://andrewschoen.github.com/django-cms-presentation

https://github.com/andrewschoen/django-cms-presentation

.. include:: _templates/pykc-logo.rst













