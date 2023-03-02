
##### _import

<!-- language: python -->
    # -*- coding: utf-8 -*-
    
    from odoo import api, fields, models, _
    from odoo.exceptions import ValidationError
    from odoo.osv import expression


##### _class
<!-- language: python -->
    class $cls$(models.Model):
        _name = '$dot_model$'
        _description = '$desc$'

        name = fields.Char()


##### _constraint
<!-- language: python -->
    @api.constraint('$field$')
    def _check_$field$(self):
        for x in self:
            if not $condition$:
                raise ValidationError(_('$message$'))


##### _onchange
<!-- language: python -->
    @api.onchange('$field_id$')
    def _onchange_$field$(self):
        if self.$field_id$:
            self.$another$ = self.$field_id$.name


##### _compute
<!-- language: python -->
    @api.depends('$dependency$')
    def _compute_$field$(self):
        for x in self:
            x.$field$ = $value$


##### _create
<!-- language: python -->
    @api.model
    def create(self, vals):
        x = super($cls$, self).create(vals)
        return x


##### _copy
<!-- language: python -->
    @api.returns('self', lambda value: value.id):
    def copy(self, default=None):
        self.ensure_one()
        default = dict(default or {})
        if 'name' not in default:
            default['name'] = _('%s (copy)') % (self.name,)
        return super($cls$, self).copy(default=default)


##### _res_config_settings
<!-- language: python -->
    class $cls$(models.TransientModel):
        _inherit = 'res.config.settings'

        $field = fields.Char(string='$label$', config_parameter='$module$.$field$')


##### _controller
<!-- language: python -->
    # -*- coding: utf-8 -*-
    from odoo import http
    from odoo.http import request


    class $cls$(http.Controller):
        @http.route('/$path$', auth='$auth$', type='json')
        def $fx$(self):
            return {}

