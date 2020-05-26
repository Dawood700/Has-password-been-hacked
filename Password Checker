import requests
import hashlib

user_input = input("Please enter the password you want to check: ") # User inputs password


def api(hash_input):
    web = "https://api.pwnedpasswords.com/range/" + hash_input # Grabs API data
    api_info = requests.get(web)
    if api_info.status_code != 200:
        return "Error, please check you api input again"
    return api_info


def hacked(hash_function, hashes):
    hash_function = (line.split(":") for line in hash_function.text.splitlines()) # Splits hash code into two parts
    for hash, times_hacked in hash_function:
        if hash == hashes:
            return times_hacked


def check(info):
    sha1 = hashlib.sha1(info.encode("utf-8")).hexdigest().upper() # Takes first 5 digits of hash and checks if password has been hacked
    k_anon, tail = sha1[:5], sha1[5:]
    response = api(k_anon)
    return hacked(response, tail)


def main():
    times_hacked = check(user_input) # Return to user whether or not their password has been hacked
    if times_hacked:
        return f"{user_input} was found {times_hacked} times"
    else:
        return f"{user_input} was not found"


print(main())
