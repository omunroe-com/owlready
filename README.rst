Owlready
========

Owlready (previously named Ontopy) is a module for ontology-oriented programming in Python 3.

**Note: Owlready is deprecated in favor to the new version, Owlready2:**
  
http://bitbucket.org/jibalamy/owlready2 (development version)
  
https://pypi.python.org/pypi/Owlready2 (stable version)

Owlready can:

 - Import and export OWL 2.0 ontologies in the OWL/XML format
   (other file formats are not yet supported).

 - Manipulates ontology classes, instances and properties transparently,
   as if they were normal Python objects.

 - Add Python methods to ontology classes.

 - Perform automatic classification of classes and instances, using the HermiT reasoner.

 - Automatically generate dialog boxes for editing ontology instances,
   using `Editobj3 <http://www.lesfleursdunormal.fr/static/informatique/editobj/index_en.html>`_.

Owlready has been created by Jean-Baptiste Lamy at the LIMICS reseach lab.
It is available under the GNU LGPL licence v3.
If you use Owlready in scientific works, **please cite the following article**:

   **Lamy JB**.
   Owlready: Ontology-oriented programming in Python with automatic classification and high level constructs for biomedical ontologies.
   **Artificial Intelligence In Medicine 2017**;80C:11-28
   
In case of troubles, questions or comments, please use this Forum/Mailing list: http://owlready.8326.n8.nabble.com


  
What can I do with Owlready?
----------------------------

Load an ontology from a local repository, or from Internet:

  >>> from owlready import *
  >>> onto_path.append("/path/to/your/local/ontology/repository")
  >>> onto = get_ontology("http://www.lesfleursdunormal.fr/static/_downloads/pizza_onto.owl")
  >>> onto.load()

Create new classes in the ontology, possibly mixing OWL restrictions and Python methods:

  >>> class NonVegetarianPizza(onto.Pizza):
  ...   equivalent_to = [
  ...     onto.Pizza
  ...   & ( restriction("has_topping", SOME, onto.MeatTopping)
  ...     | restriction("has_topping", SOME, onto.FishTopping)
  ...     ) ]
  ...   def eat(self): print("Beurk! I'm vegetarian!")

Access ontology class, and create new instances / individuals:

  >>> onto.Pizza
  pizza_onto.Pizza
  >>> test_pizza = onto.Pizza("test_pizza_owl_identifier")
  >>> test_pizza.has_topping = [ onto.CheeseTopping(),
  ...                            onto.TomatoTopping(),
  ...                            onto.MeatTopping  () ]

Export to OWL/XML file:

  >>> test_onto.save()

Perform reasoning, and classify instances and classes:

::

   >>> test_pizza.__class__
   onto.Pizza
   
   >>> # Execute HermiT and reparent instances and classes
   >>> onto.sync_reasoner()
   
   >>> test_pizza.__class__
   onto.NonVegetarianPizza
   >>> test_pizza.eat()
   Beurk! I'm vegetarian !

For more documentation, look at the doc/ and doc/examples/ directories in the source.

Changelog
---------

0.2
***

* Fix sync_reasonner and Hermit call under windows (thanks Clare Grasso)

0.3
***

* Add warnings
* Accepts ontologies files that do not ends with '.owl'
* Fix a bug when loading ontologies including concept without a '#' in their IRI
  
0.3.1
*****

* Add link to Owlready2 and Nabble forum/mailing list
* Add load_ontology_from_file()
* Add unload_all_ontologies()
* Remove debug file /tmp/sortie_hermit.txt
* Add Artificial Intelligence In Medicine scientific article in doc and Readme 


Links
-----

Owlready on BitBucket (development repository): https://bitbucket.org/jibalamy/owlready

Owlready on PyPI (Python Package Index, stable release): https://pypi.python.org/pypi/Owlready

Documentation: http://pythonhosted.org/Owlready

Forum/Mailing list: http://owlready.8326.n8.nabble.com


Contact "Jiba" Jean-Baptiste Lamy:

::

  <jean-baptiste.lamy *@* univ-paris13 *.* fr>
  LIMICS
  University Paris 13, Sorbonne Paris Cité
  Bureau 149
  74 rue Marcel Cachin
  93017 BOBIGNY
  FRANCE
