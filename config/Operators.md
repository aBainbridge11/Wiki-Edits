Operators
=========

Note - These apply to the ``rlm_files`` module only.  For operators in unlang see ``man unlang``.

Additional operators other than = may be used for the attributes in either the check item, or reply item list.

The following is a list of operators, and their meaning.

| Operator |         Example         |  Use with 'check' items (users et al), or in unlang conditions                                                                                                                                                            |  Use with 'reply' items (users et al), or in unlang update blocks      |
|----------|:------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------|
| **=**    | Attribute = Value       | Not allowed as a check item for RADIUS protocol attributes. It is allowed for server configuration attributes (Auth-Type, etc), and sets the value of on attribute, only if there is no other item of the same attribute. | As a reply item, it means "add the item to the reply list, but only if there is no other item of the same attribute."|
| **:=**   | Attribute := value      | Always matches as a check item, and replaces in the configuration items any attribute of the same name. If no attribute of that name appears in the request, then this  attribute is added.                               | As a reply item, it has an identical meaning, but for the reply items, instead of the request items.  |
| **==**   | Attribute == Value      | As a check item, it matches if the named attribute is present in the request, AND has the given value.                                                                                                                    | Not allowed as a reply item.    
| **+=**   | Attribute += Value      | Always matches as a check item, and adds the current attribute with value to the list of configuration items.                                                                                                             | As a reply item, it has an identical meaning, but the attribute is added to the reply items.    |
| **!=**   | Attribute != Value      | As a check item, matches if the given attribute is in the request, AND does not have the given value.                                                                                                                     | Not allowed as a reply item.   |
| **>**    | Attribute > Value       | As a check item, it matches if the request contains an attribute with a value greater than the one given.                                                                                                                 | Not allowed as a reply item.   |
| **>=**   | Attribute >= Value      | As a check item, it matches if the request contains an attribute with a value greater than, or equal to the one given.                                                                                                    | Not allowed as a reply item.   |
| **<**    | Attribute < Value       | As a check item, it matches if the request contains an attribute with a value less than the one given.                                                                                                                    | Not allowed as a reply item.   |
| **<=**   | Attribute <= Value      | As a check item, it matches if the request contains an attribute with a value less than, or equal to the one given.                                                                                                       | Not allowed as a reply item.   |
| **=~**   | Attribute =~ Expression | As a check item, it matches if the request contains an attribute which matches the given regular expression. This operator may only be applied to string attributes.                                                      | Not allowed as a reply item.   |
| **!~**   | Attribute !~ Expression | As a check item, it matches if the request contains an attribute which does not match the given regular expression.                                                                                                       | Not allowed as a reply item.   |
| **=***   | Attribute =* Value      | As a check item, it matches if the request contains the named  attribute, no matter what the value is.                                                                                                                    | Not allowed as a reply item.   |
| **!***   | Attribute !* Value      | As a check item, it matches if the request does not contain the named attribute, no matter what the value is.                                                                                                             | Not allowed as a reply item.   |

Examples
--------

    bob  Cleartext-Password := "hello"

Requests containing the User-Name attribute, with value "bob", will be authenticated using the password "hello".  There are no reply items, so the reply will be empty. 

    DEFAULT  Auth-Type = System
      Fall-Through = Yes

For all users reaching this entry, perform authentication against the system, unless Auth-Type has already been set.  Also, process any following entries which may match. 

    DEFAULT  Service-Type == Framed-User, Framed-Protocol == PPP
      Service-Type = Framed-User,
      Framed-Protocol = PPP,
      Fall-Through = Yes

If the request packet contains the attributes Service-Type and Framed-Protocol, with the given values, then include those attributes in the reply.

That is, give the user what they ask for.  This entry also shows how to specify multiple reply items.

See the users file supplied with the server for more examples and comments.

See Also
--------

* RADIUS [[Attributes]]
