<p align="center">
  <a href="https://www.grupoa.com.br/" target="_blank">
    <img src="https://www.grupoa.com.br/hs-fs/hubfs/logo-grupoa.png?width=136&name=logo-grupoa.png" />
  </a>
</p>

<a name="description"/>

# lti-node
<p align="center">🚀 A Launch LTI (Learning Tools Interoperability) </p>


<a name="content"/>

###  🏁 Content
<!--ts-->
   * [Description](#description)
   * [Content](#content)
   * [Install](#install)
   * [Launch LTI 1.1](#launch_lti_v1)
      * [Build Signature](#build_signature)
      * [Build Launch Form Data](#build_form_data)
   * [Status](#status)
<!--te-->

<br>
<a name="install"/>

# Install
In your package.json > dependencies:
``` bash
  "lti-node": "git+https://github.com/grupo-a/lti-node.git#<TAG_VERSION>"
```
You need to change <TAG_VERSION>. See all tags clicking <a href="https://github.com/grupo-a/lti-node.git#/tags"> here</a>.

<br>
<a name="launch_lti_v1"/>



# Launch LTI 1.1

The Launch LTI is implemented following the specification: http://www.imsglobal.org/specs/ltiv1p1/implementation-guide.

If the parameters (oauth_timestamp, oauth_signature_method, oauth_nonce, oauth_version, oauth_callback, lti_message_type, lti_version) are null, they will be generated automatically.

<a name="build_signature"/>

### Build Signature
It's a function used to generate the oauth_signature field of the LTI protocol.

Example:
``` javascript
    const { launchV1 } = require('lti-node');

    const launchData = {
        user_id                                : 'test',
        roles                                  : 'urn:lti:role:ims/lis/Instructor',
        context_label                          : 'Discipline Test',
        context_title                          : 'Discipline Test',
        context_id                             : '1',
        resource_link_id                       : '1',
        resource_link_title                    : 'Link Test',
        lis_person_name_full                   : 'ABC',
        lis_person_name_family                 : 'ABC',
        lis_person_name_given                  : 'ABC',
        lis_person_contact_email_primary       : 'abc@grupoa.com.br',
        lis_person_sourcedid                   : 'abc',
        tool_consumer_instance_guid            : 'grupoa.com.br',
        tool_consumer_info_product_family_code : 'Plataforma'
    };

    const url = 'https://grupoa.com.br/lti?param=1&param=2';
    const consumerKey = 'test';
    const secretKey = '@@123@@';
  
    const signature = launchV1.buildSignature(url, launchData, consumerKey, secretKey);
```

<a name="build_form_data"/>

### Build Launch Form Data
It's a function used to generate the oauth_signature field of the LTI protocol. It also returns all fields required for building the LTI initialization form.

Example:
``` javascript
    const { launchV1 } = require('lti-node');

    const launchData = {
        user_id                                : 'test',
        roles                                  : 'urn:lti:role:ims/lis/Instructor',
        context_label                          : 'Discipline Test',
        context_title                          : 'Discipline Test',
        context_id                             : '1',
        resource_link_id                       : '1',
        resource_link_title                    : 'Link Test',
        lis_person_name_full                   : 'ABC',
        lis_person_name_family                 : 'ABC',
        lis_person_name_given                  : 'ABC',
        lis_person_contact_email_primary       : 'abc@grupoa.com.br',
        lis_person_sourcedid                   : 'abc',
        tool_consumer_instance_guid            : 'grupoa.com.br',
        tool_consumer_info_product_family_code : 'Plataforma'
    };

    const url = 'https://grupoa.com.br/lti?param=1&param=2';
    const consumerKey = 'test';
    const secretKey = '@@123@@';
  
    const launchFormaData = launchV1.buildForm(url, launchData, consumerKey, secretKey);
```

Return:
``` javascript
    {
        action: 'https://grupoa.com.br/lti?param=1&param=2',
        properties: {
            user_id: 'test',
            roles: 'urn:lti:role:ims/lis/Instructor',
            context_label: 'Discipline Test',
            context_title: 'Discipline Test',
            context_id: '1',
            resource_link_id: '1',
            resource_link_title: 'Link Test',
            lis_person_name_full: 'ABC',
            lis_person_name_family: 'ABC',
            lis_person_name_given: 'ABC',
            lis_person_contact_email_primary: 'abc@grupoa.com.br',
            lis_person_sourcedid: 'abc',
            tool_consumer_instance_guid: 'grupoa.com.br',
            tool_consumer_info_product_family_code: 'Plataforma',
            oauth_consumer_key: 'test',
            lti_version: 'LTI-1p0',
            lti_message_type: 'basic-lti-launch-request',
            oauth_callback: 'about:blank',
            oauth_version: '1.0',
            oauth_nonce: 161184495424800,
            oauth_signature_method: 'HMAC-SHA1',
            oauth_timestamp: 1611844954,
            oauth_signature: 'KomlyEQCWk/zy6Mljiunk0BhZug='
        }
    }
```
<br>
<a name="status"/>

# Status
<h4 align="center">
	🚧  Open for contribuitions...   🚧
</h4>