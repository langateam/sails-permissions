# <img src="http://cdn.tjw.io/images/sails-logo.png" height='43px' />-permissions

[![Gitter][gitter-image]][gitter-url]
[![NPM version][npm-image]][npm-url]
[![Build status][travis-image]][travis-url]
[![Dependency Status][daviddm-image]][daviddm-url]

Comprehensive sails.js user permissions and entitlements system. Supports user authentication with passport.js, role-based permissioning, object ownership, and row-level security.

## Install
```sh
$ npm install sails-permissions sails-auth --save
```

## Quickstart

**Note:** Complete documentation available in the sails-permissions wiki: https://github.com/tjwebb/sails-permissions/wiki

### 1. configure sailsrc

```json
{
  "generators": {
    "modules": {
      "permissions-api": "sails-permissions/generator"
    }
  }
}
```

### 2. run generator

```sh
$ sails generate permissions-api
```

### 3. Set environment variables

| variable | description | default |
|:---|:---|:---|
| `ADMIN_USERNAME` | admin username | `admin` |
| `ADMIN_EMAIL` | admin user email address | `admin@example.com` |
| `ADMIN_PASSWORD` | admin user password | `admin1234` |

#### 4. update configs

#### `config/policies.js`
```js
  '*': [
    'basicAuth',
    'passport',
    'sessionAuth',
    'ModelPolicy',
    'AuditPolicy',
    'OwnerPolicy',
    'PermissionPolicy',
    'RolePolicy',
    'CriteriaPolicy'
  ],

  AuthController: {
    '*': [ 'passport' ]
  }
```

#### `config/permissions.js`
```js
module.exports.permissions = {
  /**
   * If you'd like to wait for any additional hooks to load before intializing
   * the permissions hook, add the events to wait for in this list.
   */
  afterEvent: [ 'hook:orm:loaded' ],

  /**
   * Any Controllers that are not eponymous of the Models they operate on can
   * be mapped here.
   */ 
  controllerMapping: {

   /**
    * e.g. if you want your FileController to operate under the
    * jurisdiction of the FileDescriptor model rather than the File model
    */
    FileController: 'FileDescriptor'
  },

  /**
   * Set to true to ignore unknown models, that is, custom controllers that do
   * not map to any known model, or via controllerMapping. This is not
   * recommended because it creates a security hole if these additional
   * endpoints are not secured manually by policies.
   */
  allowUnknownModelDefinitions: false
};
```

## [Complete Documentation](https://github.com/tjwebb/sails-permissions/wiki)

## License
MIT

## Maintained By
[<img src='http://i.imgur.com/zM0ynQk.jpg' height='36px'>](http://balderdash.co)

<img src='http://i.imgur.com/NsAdNdJ.png'>

[sails-logo]: http://cdn.tjw.io/images/sails-logo.png
[sails-url]: https://sailsjs.org
[npm-image]: https://img.shields.io/npm/v/sails-permissions.svg?style=flat-square
[npm-url]: https://npmjs.org/package/sails-permissions
[travis-image]: https://img.shields.io/travis/tjwebb/sails-permissions.svg?style=flat-square
[travis-url]: https://travis-ci.org/tjwebb/sails-permissions
[daviddm-image]: http://img.shields.io/david/tjwebb/sails-permissions.svg?style=flat-square
[daviddm-url]: https://david-dm.org/tjwebb/sails-permissions
[gitter-image]: http://img.shields.io/badge/+%20GITTER-JOIN%20CHAT%20%E2%86%92-1DCE73.svg?style=flat-square
[gitter-url]: https://gitter.im/tjwebb/sails-permissions
