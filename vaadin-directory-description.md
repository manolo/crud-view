# &lt;crud-view&gt;

[![Available in Vaadin_Directory](https://img.shields.io/vaadin-directory/v/manolocrud-view.svg)](https://vaadin.com/directory/component/manolocrud-view)

&lt;crud-view&gt; is a [Polymer](http://polymer-project.org) Element and a couple of Mixins providing an easy way to display, sort, filter and make modifications to a list of JSON objects.


![Screenshot of crud-view](https://raw.githubusercontent.com/manolo/crud-view/master/screenshot.gif)

## Example usage:

`my-list.html`

```
...
<dom-module id="ny-list">
  <template>

    <iron-ajax auto url="users.json" handle-as="json" last-response="{{items}}"></iron-ajax>

    <crud-view item="[[item]]">

      <vaadin-text-field slot="header" placeholder="Search ..." value="{{search}}"></vaadin-text-field>
      <vaadin-button slot="header" on-click="new" theme="primary">New Item</vaadin-button>

      <vaadin-grid slot="grid" id="grid" items="[[filter(items, search, items.*)]]" active-item="{{activeItem}}">
        <vaadin-grid-column>
          <template class="header">Email</template>
          <template>[[item.email]]</template>
        </vaadin-grid-column>
        <vaadin-grid-column>
          <template class="header">
            <vaadin-grid-sorter path="name">Name</vaadin-grid-sorter>
          </template>
          <template>[[item.name]] [[item.last]]</template>
        </vaadin-grid-column>
      </vaadin-grid>

      <template class="editor">
        <my-editor item="[[item]]" on-save="save" on-delete="delete" on-close="close"></my-editor>
      </template>
    </crud-view>
  </template>

  <script>
    class MyList extends window.CrudListMixin(Polymer.Element) {
      static get is() {
        return 'ny-list';
      }
    }
    window.customElements.define(MyList.is, MyList);
  </script>
</dom-module>
```

`my-editor.html`
```
...
<dom-module id="my-editor">
  <template>
    <vaadin-form-layout>
      <vaadin-text-field label="Email (login)" value="{{item.email}}" colspan="2" required pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$"></vaadin-text-field>
      <br>
      <vaadin-password-field label="Password" value="{{item.password}}" colspan="2" required pattern="(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{6,}"></vaadin-password-field>
    </vaadin-form-layout>
  </template>

  <script>
    class MyEditor extends window.CrudItemMixin(Polymer.Element) {
      static get is() {
        return 'my-editor';
      }
    }
    window.customElements.define(MyEditor.is, MyEditor);
  </script>
</dom-module>
```
