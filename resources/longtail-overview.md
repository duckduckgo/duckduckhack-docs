# Longtail Instant Answers

Longtails are database-backed, full text search, Instant Answers. For every query DuckDuckGo receives, each Longtail's database of articles is searched and any matching articles are used to display a paragraph of text, highlighting the portion of the article which matches the query. Developing a Longtail Instant Answer entails writing a program that generates an XML data file. This XML file describes each article, as well as some other important information discussed below. The program may be written in Perl, Python, JavaScript, or Ruby, and if necessary, will be run periodically to keep the database current.

## Structure

Longtails are similar in structure to [Fatheads](http://docs.duckduckhack.com/fathead-reference/section.html#fathead-directory-structure) with respect to downloading and processing the source data. The primary difference is that the final output needs to be XML or JSON in the following formats:

```XML
<!-- This XML declaration can be simply copied and is necessary for all longtail. -->
<?xml version="1.0" encoding="UTF-8"?>
<add allowDups="true">


<!-- Each result is contained inside a <doc> element. -->
<doc>

<!-- The title field is used in the zeroclickinfo header, and is the heaviest weighted string used for query matching. -->
<!-- The CDATA entity is used for all content that might contain unsafe data -->
<field name="title"><![CDATA[U.S. House Bill #289]]></field>

<!-- The lx_sec fields are also used for query matching, with decreasing precedence. They can be omitted. -->
<field name="l2_sec"><![CDATA[Recognizing the 50th anniversary of the National Institute of Dental Research.]]></field>
<field name="l3_sec"><![CDATA[House Committee on Commerce]]></field>
<field name="l4_sec"><![CDATA[Anniversaries, Commemorations, Congress, Congressional tributes, Dental care, Dentistry, Department of Health and Human Services, Government operations and politics, Health, Legislation, Medical research, Research centers, Science, technology, communications]]></field>

<!-- The paragraph field contains the text/HTML that will be displayed inside the zeroclickinfo box. -->
<field name="paragraph"><![CDATA[Commemorates the creation of the National Institute of Dental Research, through the National Dental Research Act, and its significant national leadership role.]]></field>

<!-- The p_count field is used to break ties on exact title matches. This should be used when the data is too long to be displayed without being broken into separate paragraphs. It can be omitted. -->
<field name="p_count">1</field>

<!-- The source should match the ID from the instant answer page you created - https://duck.co/ia/dev/pipeline -->
<field name="source"><![CDATA[instant_answer_id]]></field>

</doc>
```

```JSON
[
  {
    "title":"U.S. House Bill #289",
    "l2_sec":"Recognizing the 50th anniversary of the National Institute of Dental Research.",
    "l3_sec":"House Committee on Commerce",
    "l4_sec":"Anniversaries, Commemorations, Congress, Congressional tributes, Dental care, Dentistry, Department of Health and Human Services, Government operations and politics, Health, Legislation, Medical research, Research centers, Science, technology, communications",
    "p_count":1,
    "source":"instant_answer_id"
  }
]
```

(This section is still growing! Know what should go here? Then **please** [contribute to the documentation]( https://github.com/duckduckgo/duckduckhack-docs/)!)
