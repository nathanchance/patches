diff --git a/arch/arm64/include/asm/futex.h b/arch/arm64/include/asm/futex.h
index 1943cf623366..c5bc52e47f6a 100644
--- a/arch/arm64/include/asm/futex.h
+++ b/arch/arm64/include/asm/futex.h
@@ -48,17 +48,17 @@ do {									\
 } while (0)
 
 static inline int
-futex_atomic_op_inuser (int encoded_op, u32 __user *_uaddr)
+futex_atomic_op_inuser(unsigned int encoded_op, u32 __user *_uaddr)
 {
 	int op = (encoded_op >> 28) & 7;
 	int cmp = (encoded_op >> 24) & 15;
-	int oparg = (encoded_op << 8) >> 20;
-	int cmparg = (encoded_op << 20) >> 20;
+	int oparg = (int)(encoded_op << 8) >> 20;
+	int cmparg = (int)(encoded_op << 20) >> 20;
 	int oldval = 0, ret, tmp;
 	u32 __user *uaddr = __uaccess_mask_ptr(_uaddr);
 
 	if (encoded_op & (FUTEX_OP_OPARG_SHIFT << 28))
-		oparg = 1 << oparg;
+		oparg = 1U << (oparg & 0x1f);
 
 	if (!access_ok(VERIFY_WRITE, uaddr, sizeof(u32)))
 		return -EFAULT;
