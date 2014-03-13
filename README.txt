stratum-mining-darkcoin
=======================

diff for stratum-mining-darkcoin


# conf.py

-COINDAEMON_ALGO = 'scrypt'    # The available options are:  scrypt, sha256d, scrypt-jane, skeinhash, and quark
+COINDAEMON_ALGO = 'quark'    # The available options are:  scrypt, sha256d, scrypt-jane, skeinhash, and quark



-POOL_TARGET = 32                # Pool-wide difficulty target int >= 1
+POOL_TARGET = 0.010
 


-VDIFF_MIN_TARGET = 16           # Minimum target difficulty 
-VDIFF_MAX_TARGET = 1024         # Maximum target difficulty 
+VDIFF_MIN_TARGET = 0.008           # Minimum target difficulty 
+VDIFF_MAX_TARGET = 0.08


# lib/halfnode.py
@@ -28,7 +28,7 @@
     log.debug("########################################### LoadingScrypt jane #########################################################")
 elif settings.COINDAEMON_ALGO == 'quark':
     log.debug("########################################### Loading Quark Support #########################################################")
-    import quark_hash
+    import dark_hash
 elif settings.COINDAEMON_ALGO == 'skeinhash':
     import skeinhash
 
@@ -293,7 +293,7 @@
                 r.append(struct.pack("<I", self.nTime))
                 r.append(struct.pack("<I", self.nBits))
                 r.append(struct.pack("<I", self.nNonce))
-                self.quark = uint256_from_str(quark_hash.getPoWHash(''.join(r)))
+                self.quark = uint256_from_str(dark_hash.getPoWHash(''.join(r)))
              return self.quark


# lib/template_registry.py
@@ -8,7 +8,7 @@
 elif settings.COINDAEMON_ALGO  == 'scrypt-jane':
     scryptjane = __import__(settings.SCRYPTJANE_NAME) 
 elif settings.COINDAEMON_ALGO == 'quark':
-    import quark_hash
+    import dark_hash
 elif settings.COINDAEMON_ALGO == 'skeinhash':
     import skeinhash
 else: pass
 
 
 @@ -250,7 +267,7 @@
       		else: 
       		     hash_bin = scryptjane.getPoWHash(''.join([ header_bin[i*4:i*4+4][::-1] for i in range(0, 20) ]), int(ntime, 16))
         elif settings.COINDAEMON_ALGO == 'quark':
-            hash_bin = quark_hash.getPoWHash(''.join([ header_bin[i*4:i*4+4][::-1] for i in range(0, 20) ]))
+            hash_bin = dark_hash.getPoWHash(''.join([ header_bin[i*4:i*4+4][::-1] for i in range(0, 20) ]))
 	elif settings.COINDAEMON_ALGO == 'skeinhash':
             hash_bin = skeinhash.skeinhash(''.join([ header_bin[i*4:i*4+4][::-1] for i in range(0, 20) ]))
         else:
         

#dark_hash = x11_hash
use : https://github.com/chaeplin/p2pool-drk/tree/master/py_module/darkcoin-hash-python
