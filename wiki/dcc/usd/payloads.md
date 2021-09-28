# Payloads

Payloads are similar to references however also allow for the data to be loaded and unloaded within the stage (helps avoid incurring the composition costs).

Anytime we move anything below the payload level above the payload (within the composition stack), this process is called **lofting**. So when the payload is unloaded, we still have access to the lofted information.
