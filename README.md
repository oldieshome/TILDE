# TILDE
**T**rim **I**ndented **L**ayout for **E**ntity **D**escription. **Trim** implying a simple, economical method for encoding information in text files. **TILDE** can be used to describe bibliographic, museum, and similar information entities, and to record information such as terminologies in a hierarchical fashion. The aim of TILDE is to minimse the encoding used to structure the content of the description so that the description can be easily read and understood in its raw form and, as a result, can be created and edited by basic software such as a text editor.

The basic structure is as follows :

A TILDE description is a text stream which uses **descriptors** to describe an entity. Descriptors comprise a label and a value, and for each value there may be subsiduary descriptors arranged in a hierarchy which is indicated by indentation, like YAML. An example of a text stream is a sequentially-read text file.

Descriptors can be one of three types: an **attribute** of the entity, a **property** of the description or attribute value or a **cluster** attribute which brings together the attributes of an entity. Properties are different in that they apply to the parent descriptor value, for example specifying language, and apply to all attribute values down the hierarchy of the parent value unless over-ridden by another property definition at a lower level.

These descriptors are lines of text commencing and encoded as follows :

1. Zero to many spaces indicating the indentation level. Properties at the zero level apply to the whole text stream

2. A label composed of these characters   *A-Za-z0-9.:_-|#~* Attribute and cluster labels must end with a ~ (tilde character). By convention cluster labels are attributes which start with an upper-case character and edn with a ~ . Property labels commence and end with ~ .

3. Zero to many spaces.

4. A value which is text. The text may be formatted in a standard way to represent other types of value, for example a number. The value may continue over the following lines until a line with the encoding of a descriptor.

Here is an example of a TILDE description :

    ~language~ english
    ~updated~ 2019-08-23T09:55:07 
    InformationResource~
        title~ Yorkshire cotton
            sub-title~ The Yorkshire cotton industry, 1780-1835
        written~
            by~ George Ingle       
        is-a~ book
            comprises~ text, illustrations, photographs, sources, gazetteer
        published~
           by~ Carnegie Publishing Limited
           location~ Preston, United Kingdom
           date~ 1997
           form~ soft cover; print, on paper; 279p
           identifier~ ISBN 1-85936-0820-9
        about~
            location~ Yorkshire, United Kingdom
            subject~ history, cotton industry
            period~ 1780 - 1835
            keywords~ industrial revolution, surveys, water power, 
                      steam power, machinery, mill construction, capital, 
                      labour supply

There are some special descriptors :

    ~ value       This is used to indicate an entry in a list of values for the label ~.
    ~~ value      This indicates a repeat of the previous label. The value is added to the list of values
                    of that previous label.
    ~~~ label~ description  This introduces a text definition of the descriptor label~ . Other child 
                    attributes can define other attributes of the descriptor, for example the content
                    of format.
    ~~~~ source   This indicates a source, for example a filename or url from where a new text stream can 
                    be loaded at this point in the text stream.
    |~ value | value | etc.  This creates an entry in a list for the label |~ and implies the value is 
                    split up into components separated by the | character. This feature can be used to 
                    create a table of values.
                    
In addition to these special descriptors lines commencing with *|space* and *#space* have a special meaning :

    | This line of text commences on a new line
    # This line of text is a comment and is ignored in the data model.
    
Where a value comprises consecutive lines of text are run together and any initial space characters in the following line are replaced by a single space. Also, a blank line in the text will mean the following line of the value starts on a new line.

The basic data model for a descriptor is:

    a label
    a list of associated values 
        for each value, an index of child descriptors
    the parent descriptor

For further information : https://oldieshome.org.uk/TechNotes/TILDE


