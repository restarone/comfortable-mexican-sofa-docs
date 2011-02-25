# Page Tag

Page tag is defines a piece of content that is displayed during page rendering. Each piece of content has a unique identifier, or `label` and an optional format. Format defines what kind of form field needs to be used during CMS Page creation.

    CMS Layout                          CMS Page Creation                   Final Result
    ╔═══════════════════════════╗       ╔═══════════════════════════╗       ╔═══════════════════════════╗
    ║  <html>                   ║       ║                           ║       ║  <html>                   ║
    ║    {{cms:page:header }}   ║       ║ [ form field for header ] ║       ║    header content         ║
    ║    {{cms:page:body }}     ║  ==>  ║ [ form field for body   ] ║  ==>  ║    body content           ║
    ║    {{cms:page:footer }}   ║       ║ [ form field for footer ] ║       ║    footer content         ║
    ║  </html>                  ║       ║                           ║       ║  </html>                  ║
    ╚═══════════════════════════╝       ╚═══════════════════════════╝       ╚═══════════════════════════╝

### Available formats

<table>
  <tr>
    <td><em>{{ cms:page:content }}</em></td>
    <td><strong>Text</strong></td>
    <td>Format parameter can be omitted. It defaults to *text*</td>
  </tr>
  <tr>
    <td>{{ cms:page:content:text }}</td>
    <td>Text</td>
    <td>A plain-text textarea. With html/css/js code highlighting provided via CodeMirror</td>
  </tr>
  <tr>
    <td>{{ cms:page:content:rich_text}}</td>
    <td>RichText</td>
    <td>WYSIWYG editor (TinyMCE) will be used.</td>
  </tr>
  <tr>
    <td>{{ cms:page:content:string }}</td>
    <td>String</td>
    <td>Sometimes you need a short text entry. This will render a text field.</td>
  </tr>
  <tr>
    <td>{{ cms:page:content:datetime }}</td>
    <td>DateTime</td>
    <td>Textfield, with Datetime selection widget.</td>
  </tr>
  <tr>
    <td>{{ cms:page:content:integer }}</td>
    <td>Integer</td>
    <td>Input with 'number' type will be rendered. You can only type numbers in there.</td>
  </tr>
</table>

Formats only control how content gets populated during CMS Page creation. They do not control how that content is displayed on final page render.

  