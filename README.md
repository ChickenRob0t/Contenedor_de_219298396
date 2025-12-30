
class BadConfigRootError(Exception):
    """Has bad routing xml"""
    pass

def check_prop():
    if datetime.datetime(2025, 6, 1)>datetime.datetime.now():
        pass    
    else:
        raise BadConfigRootError("It dont works correctly, try using another caracter design")
        raise 

def cracking_n():
    check_prop()
    print('Algo más haciéndose así')
