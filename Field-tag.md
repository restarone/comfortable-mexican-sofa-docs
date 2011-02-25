# Field Tag

Field Tag is special tag that behaves similarly to [[Page Tag]] but with one distinct difference: it does NOT get rendered on the page.

    CMS Layout                          CMS Page Creation                   Final Result
    ╔═══════════════════════════╗       ╔═══════════════════════════╗       ╔═══════════════════════════╗
    ║  <html>                   ║       ║                           ║       ║  <html>                   ║
    ║    {{cms:field:meta }}    ║       ║ [ form field for meta ]   ║       ║    body content           ║
    ║    {{cms:page:body }}     ║  ==>  ║ [ form field for body ]   ║  ==>  ║  </html>                  ║
    ║  </html>                  ║       ║                           ║       ║                           ║
    ╚═══════════════════════════╝       ╚═══════════════════════════╝       ╚═══════════════════════════╝
    
This is very useful if you want to output this Field content somewhere inside your application. See [[Accessing CmsPage content directly]] for examples.

### Available formats

<table>
  <tr>
    <td><em>{{ cms:page:content }}</em></td>
    <td><strong>String</strong></td>
    <td>Format parameter can be omitted. It defaults to :string</td>
  </tr>
  <tr>
    <td><em>{{ cms:page:content:string }}</em></td>
    <td><strong>String</strong></td>
    <td>Generally Fields are used for short bits of text</td>
  </tr>
  <tr>
    <td><em>{{ cms:page:content:text }}</em></td>
    <td><strong>Text</strong></td>
    <td>A plain-text textarea. With html/css/js code highlighting provided via CodeMirror</td>
  </tr>
  <tr>
    <td><em>{{ cms:page:content:datetime }}</em></td>
    <td><strong>DateTime</strong></td>
    <td>Textfield, with Datetime selection widget.</td>
  </tr>
  <tr>
    <td><em>{{ cms:page:content:integer }}</em></td>
    <td><strong>Integer</strong></td>
    <td>Input with 'number' type will be rendered. You can only type numbers in there.</td>
  </tr>
</table>
