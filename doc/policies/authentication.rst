.. _authentication_policies:

Authentication policies
-----------------------

.. index:: authentication policies

The scope *authentication* gives you more detailed
possibilities to authenticate the user or to define 
what happens during authentication.

Authentication polcies take the realm, the user
and the client into account.

Technically the authentication policies apply
to the :ref:`validate_controller`.

The following actions are available in the scope 
*authentication*:

smstext
~~~~~~~

type: string

This is the text that is sent via SMS to the user trying to
authenticate with an SMS token.
You can use the tags *<otp>* and *<serial>*.


otppin
~~~~~~

type: int

This action defines how the fixed password part during
authentication should be validated.
Each token has its own OTP PIN, but you can choose 
how the authentication should be processed:

``otppin=0``

   This is the default behaviour. The user needs to
   pass the OTP PIN concatenated with the OTP value.

``otppin=1``

   The user needs to pass the user store password
   concatenated with the OTP value. It does not matter
   if the OTP PIN is set or not.
   If the user is located in an Active Directory the user
   needs to pass his domain password together with the
   OTP value.

.. note:: The domain password is checked with an LDAP
   bind right at the moment of authentication. 
   So if the user is locked or the password was
   changed authentication will fail.

``otppin=2``

   The user does not have to pass any fixed password.
   Authentication is only done via the OTP value.

autosms
~~~~~~~

type: bool

A new OTP value will be sent via SMS if the user authenticated
successfully with his SMS token. Thus the user does not
have to trigger a new SMS when he wants to login again.

passthru
~~~~~~~~

.. index:: passthru

type: bool

If the user has no token assigned, he will be authenticated
against the UserIdResolver, i.e. he needs to provide the
LDAP- or SQL-password.

.. note:: This is a good way to do a smooth enrollment.
   Users having a token enrolled will have to use the 
   token, users not having a token, yet, will be able
   to authenticate with their domain password.

.. warning:: If the user has the right to delete his
   tokens in selfservice portal, the user could 
   delete all his tokens and then authenticate with
   his static password again.

passOnNoToken
~~~~~~~~~~~~~

.. index:: passOnNoToken

type: bool

If the user has no token assigned an authentication request
for this user will always be true.

.. warning:: Only use this if you know exactly what
   you are doing.

qrtanurl
~~~~~~~~

type: string

This is the URL for the half automatic mode of the QR token.
To this URL the TAN/OTP value will be pushed.

challenge_response
~~~~~~~~~~~~~~~~~~

type: string

This is a list of token types for which challenge response can
be used during authentication.

