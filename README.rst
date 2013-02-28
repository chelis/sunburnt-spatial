Sunburnt
========

Sunburnt is a Python-based interface for working with the `Apache Solr
<http://lucene.apache.org/solr/>`_ search engine.

It was written by Toby White <toby@timetric.com> for use in the `Timetric
platform <http://timetric.com>`_.

Please send queries/comments/suggestions to the `mailing list
<http://groups.google.com/group/python-sunburnt>`_.

Bugs can be filed on the `issue tracker <https://github.com/tow/sunburnt/issues>`_.

It's tested with Solr 1.4.1 and 3.1; previous versions were known to work
with 1.3 and 1.4 as well.

Full documentation can be found at http://opensource.timetric.com/sunburnt/index.html.

Dependencies
============

- Requirements:

  * `httplib2 <http://code.google.com/p/httplib2/>`_
  * `lxml <http://lxml.de>`_

- Strongly recommended:

  * `mx.DateTime <http://www.egenix.com/products/python/mxBase/mxDateTime/>`_

    Sunburnt will happily deal with dates stored either as Python datetime
    objects, or as mx.DateTime objects. The latter are preferable,
    having better semantics and a wider representation range. They will
    be used if present, otherwise sunburnt will fall back to Python
    datetime objects.

  * `pytz <http://pytz.sourceforge.net>`_

    If you're using native Python datetime objects with Solr (rather than
    mx.DateTime objects) you should also have pytz installed to guarantee
    correct timezone handling.

- Optional (only to run the tests)

  * `nose <http://somethingaboutorange.com/mrl/projects/nose/>`_

Additions
=========
Forked by Károly "Charles" Nagy to add some essential feature for other projects.

- Range facets:

    Every range field can be set separately in order to fulfill the requirements. 
    The facet_ranger.update() method takes a dictionary with the field names and 
	the essential parameters (start, end and gap)
	
	Example:
	
{{{
from sunburnt import SolrInterface
si = SolrInterface('http://some.url:8983/solr/')
si.query('Query')
si.facet_ranger.update({
    'price':
        {'range.start': 1, 'range.end': 99999, 'range.gap': 5000}
})
}}}
	
	* `More info <http://charlesnagy.info/it/python/solr-python-interface-sunburnt-fork>`_
	
- Spatial index:

    Spatial filtering is now available through sunburnt with filter_spatial function. 
	
	Example:
	
{{{
from sunburnt import SolrInterface
SOLR_URL = 'http://some.url:8983/solr/'
_s = SolrInterface(SOLR_URL)
_s.query('*')
_s.filter_spatial(latlon=(47.4775899,18.8108992), distance=10)
}}}

