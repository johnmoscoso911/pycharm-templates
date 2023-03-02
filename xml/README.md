##### _xml
Applicable in XML: XML text
###### template text:
    <?xml version="1.0" encoding="utf-8"?>
    <odoo>

    </odoo>


##### _form
Applicable in XML: XML text, XML tag.
Variables...
- **dot_model**
- **dash_model**, regularExpression(dot_model, "\\\\.", "_")
- **title**
###### template text:
    <!-- FORM VIEW -->
    <record id="$dash_model$_form_view" model="ir.ui.view">
        <field name="name">$dot_model$.form</field>
        <field name="model">$dot_model$</field>
        <field name="arch" type="xml">
            <form string="$title$">
                <field name="active" invisible="1"/>
                <header/>
                <sheet>
                    <div class="oe_button_box">
                        <widget name="web_ribbon" title="Archived" bg_color="bg-danger"
                                    attrs="{'invisible': [('active', '=', True)]}"/>
                    </div>
                    <div class="oe_title">
                        <label class="oe_edit_only" for="name" string="Name"/>
                        <h1>
                            <field name="name" placeholder="Name"/>
                        </h1>
                    </div>
                    <group>
                        <group>
                        </group>
                        <group/>
                    </group>
                    <notebook>
                        <page string="">
                            <group>
                                <group>
                                </group>
                                <group/>
                            </group>
                        </page>
                        <page string="">
                            <field name="_id" widget="many2one" mode="tree">
                                <tree editable="bottom">
                                    <field name=""/>
                                </tree>
                            </field>
                        </page>
                        <page string="Description">
                            <field name="description" widget="html" nolabel="1"/>
                        </page>
                    </notebook>
                </sheet>
            </form>
        </field>
    </record>


##### _tree
Applicable in XML: XML text, XML tag.
Variables...
- **dot_model**
- **dash_model**, regularExpression(dot_model, "\\\\.", "_")
- **title**
###### template text:
    <!-- TREE VIEW -->
    <record id="$dash_model$_list_view" model="ir.ui.view">
        <field name="name">$dot_model$.list</field>
        <field name="model">$dot_model$</field>
        <field name="arch" type="xml">
            <tree string="$title$">
                <field name="name"/>
                <field name="" invisible="1"/>
            </tree>
        </field>
    </record>


##### _search
Applicable in XML: XML text, XML tag.
Variables...
- **dot_model**
- **dash_model**, regularExpression(dot_model, "\\\\.", "_")
- **title**
###### template text:
    <!-- SEARCH VIEW -->
    <record id="$dash_model$_filter_view" model="ir.ui.view">
        <field name="name">$dot_model$.filter</field>
        <field name="model">$dot_model$</field>
        <field name="arch" type="xml">
            <search string="$title$">
                <field name="name"/>
                <field name=""/>
                <!-- <filter domain="[('', '=', context_today().strftime('%Y'))]" string="" name="" help=""/> -->
                <separator/>
                <filter string="Archived" name="inactive" domain="[('active', '=', False)]"/>
                <group expand="0" string="Group By">
                    <filter name="group_" string="" context="{'group_by': ''}"/>
                </group>
            </search>
        </field>
    </record>


##### _kanban
Applicable in XML: XML text, XML tag.
Variables...
- **dot_model**
- **dash_model**, regularExpression(dot_model, "\\\\.", "_")
- **another**
- **m2m**
###### template text:
    <!-- KANBAN VIEW -->
    <record id="$dash_model$_kanban_view" model="ir.ui.view">
        <field name="name">$dot_model$.kanban</field>
        <field name="model">$dot_model$</field>
        <field name="arch" type="xml">
            <kanban class="o_kanban_mobile">
                <field name="name"/>
                <field name="$another$"/>
                <field name="$m2m$_ids"/>
                <templates>
                    <t t-name="kanban-box">
                        <div t-attf-class="oe_kanban_card or oe_kanban_content oe_kanban_global_click">
                            <!-- <div class="o_kanban_record_top mb16">
                                <div class="o_kanban_record_headings mt4">
                                    <strong class="o_kanban_record_title">
                                        <span>
                                        </span>
                                    </strong>
                                </div>
                                <strong>
                                </strong>
                            </div> -->
                            <div>
                                <strong class="o_kanban_record_title">
                                    <span><field name="name"/></span>
                                </strong>
                            </div>
                            <div>
                                <span class="o_kanban_record_subtitle"><field name="$another$"/></span>
                            </div>
                            <div>
                                <field name="$m2m$_ids" widget="many2many_tags" options="{'color_field': 'color'}"/>
                            </div>
                            <div class="o_kanban_record_bottom">
                                <div class="oe_kanban_bottom_left"/>
                                <div class="oe_kanban_bottom_right"/>
                            </div>
                        </div>
                    </t>
                </templates>
            </kanban>
        </field>
    </record>


##### _act_window
Applicable in XML: XML text, XML tag.
Variables...
- **dot_model**
- **dash_model**, regularExpression(dot_model, "\\\\.", "_")
- **title**
- **low_title**, lowercaseAndDash(title)
- **seq**
###### template text:
    <!-- ACTION -->
    <record id="$dash_model$_action_all" model="ir.actions.act_window">
        <field name="name">$title$</field>
        <field name="type">ir.actions.act_window</field>
        <field name="res_model">$dot_model$</field>
        <field name="view_mode">kanban,tree,form</field>
        <field name="context">{}</field>
        <field name="help" type="html">
            <p class="o_view_nocontent_smiling_face">
                Create a new $low_title$
            </p>
        </field>
    </record>
    <menuitem id="menu_$dash_model$" action="$dash_model$_action_all" sequence="$seq$" groups="base.group_user"/>