
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


##### _name_search

<!-- language: python -->
    @api.model
    def _name_search(self, name, args=None, operator='ilike', limit=100, name_get_uid=None):
        if not args:
            args = []
        if name:
            domain = [
                '|',
                ('name', operator, name),
                ('$field$', operator, name)
            ]
            domain = expression.AND([args, domain])
            _ids = list(self._search(domain, limit=limit, access_rights_uid=name_get_uid))
        else:
            _ids = self._search(args, limit=limit, access_rights_uid=name_get_uid)
        return _ids


##### _name_get

<!-- language: python -->
    def name_get(self):
        res = []
        for $obj$ in self:
            name = $obj$.name
            if $obj$.$field$:
                name = '%s - %s' % (name, $obj$.$field$)
            res.append(($obj$.id, name))
        return res


##### _controller

<!-- language: python -->
    # -*- coding: utf-8 -*-

    from odoo import http
    from odoo.http import request


    class $cls$(http.Controller):
        @http.route('/$path$', auth='$auth$', type='json')
        def $fx$(self):
            return {}


##### _wizard

<!-- language: python -->
    # -*- coding: utf-8 -*-

    from odoo import api, fields, models, _
    from odoo.exceptions import UserError
    from odoo.tools.misc import format_date


    class $cls$(models.TransientModel):
        _name = '$dot_model$'
        _description = '$desc$'

        def do_action(self):
            # action = {
            #    'name': _('Title'),
            #    'res_model': 'model',
            #    'view_mode': 'tree,form',
            #    'type': 'ir.actions.act_window',
            #    'views': [(self.env.ref('module.xml_id'), 'tree'), (False, 'form')]
            # }
            # action = {
            #    'name': _('Title'),
            #    'res_model': 'model',
            #    'view_mode': 'form',
            #    'view_type': 'form',
            #    'type': 'ir.actions.act_window',
            #    'res_id': obj.id
            # }
            action = {'type': 'ir.actions.act_window_close'}
            return action