# bash || && 后面接多命令

suc echo 123 && {echo 123; echo 456}

fail echo 123 || {echo 123; echo 456}
