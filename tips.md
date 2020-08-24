# Tips

1. Keystone, Fernet tokens, token_flush
 - In recent osp releases, we use fernet tokens instead of uuid tokens. With Fernet token, we do not persist token in DB, so we do not need token_flush job for keystone anymore.

